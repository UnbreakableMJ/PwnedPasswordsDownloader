# What is haveibeenpwned-downloader?
`haveibeenpwned-downloader` is a [dotnet tool](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools) to download all Pwned Passwords hash ranges and save them offline so they can be used without a dependency on the k-anonymity API

## Prerequisites

### Docker: 
```
docker pull mcr.microsoft.com/dotnet/sdk:6.0
```

### Debian:
```
wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
  sudo dpkg -i packages-microsoft-prod.deb && \
  rm packages-microsoft-prod.deb && \
  sudo apt update && \
  sudo apt install -y dotnet-sdk-6.0
```

### OpenSuSE:
```
sudo zypper install dotnet-sdk-5.0
```

### Ubuntu: 
See https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#im-using-ubuntu-2204-2210-or-2304-and-i-only-need-net-60-or-net-70

### Windows: 
```
winget install Microsoft.DotNet.SDK.6
```

# Installation

## How to install
1. Open a terminal window
2. Run ```dotnet tool install --global haveibeenpwned-downloader```

### Troubleshooting
If the installer is unable to resolve the package, then you can run the following and then try again.
```
dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org
```

# Usage Examples

### Download all SHA1 hashes to a single txt file called `pwnedpasswords.txt`
```haveibeenpwned-downloader pwnedpasswords```

### Download all SHA1 hashes to individual txt files into a custom directory called `hashes`
```haveibeenpwned-downloader pwnedpasswords -s false```

### Download all NTLM hashes to a single txt file called `pwnedpasswords_ntlm.txt`
```haveibeenpwned-downloader -n pwnedpasswords_ntlm```


# Additional parameters

| Parameter   | Default value | Description |
|-------------|---------------|-------------|
| -s/--single | true | Determines wether to download hashes to a single file or as individual .txt files into another directory |
| -p/--parallelism | Same as `Environment.ProcessorCount` | Determines how many hashes to download at a time |
| -o/--overwrite | false | Determines if output files should be overwritten or not |
| -n | (none) | When set, the downloader fetches NTLM hashes instead of SHA1 |

# Additional usage examples
## Download all hashes to individual txt files into a custom directory called `hashes` using 64 threads to download the hashes
```haveibeenpwned-downloader hashes -s false -p 64```
## Download all hashes to a single txt file called `pwnedpasswords.txt` using 64 threads, overwriting the file if it already exists
```haveibeenpwned-downloader pwnedpasswords -o -p 64```
