---
title: Certificate based authentication for devices against L7 load balancers
date: 2023-08-07
tags: ["azure","blog"]
image : "/img/posts/ai-generated-certificate-based-authentication.png"
Description  : "It’s a fast and static website generator w ritten in the Go language. Websites built with Hugo can be hosted anywhere from GitHub..."
featured: true
---

```powershell
# Define variables
$rootCertName = "My Root CA"
$certName = "My Signed Certificate"
$certPath = "Cert:\CurrentUser\My"
$certStore = "Cert:\CurrentUser\Root"
$PFXPassword = 'HelloKitty123!'

# Create a new self-signed certificate and install it in the \My store (needed for signing)
$rootCert = Get-ChildItem -Path $certStore | Where-Object { $_.Subject -eq "CN=$rootCertName" }
if (-not $rootCert) {
    $rootCert = New-SelfSignedCertificate `
        -DnsName $rootCertName `
        -Subject "CN=$rootCertName" `
        -CertStoreLocation $certPath `
        -Type Custom `
        -KeySpec Signature `
        -KeyUsage CertSign, CRLSign, DigitalSignature, KeyEncipherment `
        -FriendlyName $rootCertName `
        -NotAfter (Get-Date).AddYears(10) `
        -TextExtension @("2.5.29.19={text}CA=true")
}

#export the Public Key of the Root CA in base64 format
Set-Content -Path "$rootCertName.cer" -Value $([convert]::tobase64string($rootCert.RawData)) -Encoding ascii

# Install the certificate in the root store, if you want to try to authenticate from the current machine
$store = New-Object System.Security.Cryptography.X509Certificates.X509Store("Root", "CurrentUser" )
$store.Open([System.Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)
$store.Add($rootCert)
$store.Close()

# Create a new certificate and sign it with the CA created above
$signedCertificate = New-SelfSignedCertificate `
    -DnsName $certName `
    -CertStoreLocation $certPath `
    -Type Custom `
    -KeySpec Signature `
    -Subject "CN=$certName" `
    -KeyUsage DigitalSignature, KeyEncipherment `
    -FriendlyName $certName `
    -NotAfter (Get-Date).AddYears(1) `
    -Signer $rootCert

# Export the certificate for later usage in code
$signedCertificate | Export-PfxCertificate -Password $(ConvertTo-SecureString $PFXPassword -Force -AsPlainText) -FilePath "$certName.pfx"
```



```csharp
using System;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;

namespace CertificateBasedAuthentication
{
    class Program
    {
        static void Main(string[] args)
        {
            string pathToCertificate = "C:\\Users\\bgrozoiu\\My Signed Certificate.pfx";
            string certificatePassword = "HelloKitty123!";
            string apiEndpoint = "https://aag.itdelivery.ro";

            // Load the certificate from a file
            X509Certificate2 certificate = new X509Certificate2(pathToCertificate, certificatePassword);

            // Create a new HttpClientHandler and set the client certificate
            HttpClientHandler handler = new HttpClientHandler();
            handler.ClientCertificates.Add(certificate);

            // Create a new HttpClient with the handler
            HttpClient client = new HttpClient(handler);

            // Set the base address of the API
            client.BaseAddress = new Uri(apiEndpoint);

            // Make a GET request to the API
            HttpResponseMessage response = client.GetAsync("api/web").Result;

            // Check if the request was successful
            if (response.IsSuccessStatusCode)
            {
                // Read the response content
                string content = response.Content.ReadAsStringAsync().Result;

                // Display the response content
                Console.WriteLine(content);
            }
            else
            {
                // Display the error status code
                Console.WriteLine("Error: " + response.StatusCode);
            }

            // Wait for user input before closing the console window
            Console.ReadLine();
        }
    }
}
```