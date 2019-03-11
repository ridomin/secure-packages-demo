# secure packages demo

This repo contains a sample `nuget.config` file with advanced security requirements based on NuGet package signatures

## Trusted Signers

The trusted signers feature was announced in the [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html) introducing trust policies for nuget

## Trusting Repository Signatures from NuGet.org

The configuration file includes the fingerprint for the NuGet.org repository signature

```xml
<repository name="NuGet.org" serviceIndex="https://api.nuget.org/v3/index.json">
   <certificate fingerprint="0e5f38f57dc1bcc806d8494f4f90fbcedd988b46760709cbeec6f4219aa6157d" 
                hashAlgorithm="SHA256" />
      <owners>Microsoft</owners>
</repository>
```

>Note that we are only trusting packages owned by Microsoft

To trust an specific author based on the author signature, whether it's acquired from NuGet.org or any other repository

```xml
    <author name="Rido_CA_">
      <certificate fingerprint="518F74AE79E44C7451FB5013E63D46BFF967A11AA13CD8F4586C57059AE900C9"
                   hashAlgorithm="SHA256" />
    </author>
```

## Trusting Self Signed Certificates

In this demo, the package `.\_pkgs\System.Rido.1.0.8-pre.nupkg` is signed with a self-signed certificate.

NuGet policies allow to trust a certificate that does not chain to a trusted root by enabling the `allowUntrustedRoot` attribute

```xml
<author name="Ringo">
  <certificate fingerprint="F6B6EF6F6A9C60BC4B0A181A140C8CF1BA849B30C500FDD44F77A4C1672904B3"
               hashAlgorithm="SHA256" 
               allowUntrustedRoot="true" />
    </author>
```

>The self-signed certificate is associated with my [CertCentral](https://certcentral.x509.online/home/UserCerts/ridomin) account.