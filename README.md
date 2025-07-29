# Cloudflare-Go

> [!CAUTION]
> This fork is offered as-is, and without guarantees. It is expected that changes in the code, repository, and API occur in the future. We recommend taking caution before using this library in production.

## Overview

This is an experimental fork of Go that patches the TLS stack to support modern cryptographic features and protocols. The fork maintains compatibility with standard Go while adding enhanced security capabilities.

This fork provides support for:

1. [Encrypted ClientHello (ECH)](https://blog.cloudflare.com/encrypted-client-hello/)
2. [Post-quantum key agreement](https://blog.cloudflare.com/post-quantum-for-all/)
3. [Delegated Credentials](https://blog.cloudflare.com/keyless-delegation/)
4. Post-quantum certificates
5. Configuration of keyshares sent in ClientHello with `tls.Config.ClientCurveGuess`.

## Build Instructions

### Quick Start

```bash
git clone https://github.com/trustonedge/cloudflare-go
cd go/src
./make.bash
```

### What happens during build

The `make.bash` script builds a complete Go toolchain from source:

1. Uses your existing Go installation as a **bootstrap compiler**
2. Creates a new Cloudflare Go installation
3. Compiles all Go tools (`go`, `gofmt`, `go vet`, etc.)
4. Installs everything in the local `bin` directory

## Usage

### Setting up your environment

After building, you'll have two Go installations:

- **System Go**: Your original Go installation (standard Go), `/usr/local/go`
- **Cloudflare Go**: Cloudflare's fork with post-quantum crypto support, ` /home/ubuntu/cloudflare-go`

To use Cloudflare's Go version, update your PATH:

```bash
# Add to your ~/.bashrc
export PATH="/path/to/cloudflare-go/bin:$PATH"
# e.g. export PATH="/home/ubuntu/cloudflare-go/bin:$PATH"

# Apply changes
source ~/.bashrc
```

### Verification

Confirm you're using the correct version:

```bash
which go
go version
```

### Build tag compatibility

To maintain compatibility with upstream Go, this fork uses the `cfgo` build tag. This allows you to use the same codebase with both standard Go and this enhanced fork.

## Benefits

This method gives you access to Cloudflare's modifications (like post-quantum TLS support) while keeping the familiar `crypto/tls` import path. Now when you use `import "crypto/tls"` in your code, you'll get Cloudflare's enhanced version instead of the standard library.
