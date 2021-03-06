# Introduction

Builders that are managed by the coordinator (VMs running on GCE or reverse buildlets, such as the new OS X builders) are listed here:

http://farmer.golang.org/builders

For design details about the coordinator, see http://golang.org/s/builderplan

Older-style builders are listed below. These builders are configured and run manually. The goal is to migrate as many as possible over to the new system.

| **title** | **description** | **owner** | **notes** |
|:----------|:----------------|:----------|:----------|
| linux-arm64-canonical | ARMv8 | @davecheney | Ubuntu 14.04 |
| linux-arm64-linaro | ARMv8 | @davecheney | Ubuntu 14.04.2 |
| linux-ppc64le-canonical | POWER8 little endian | @davecheney | Ubuntu 14.04 |
| android-arm-crawshaw | Nexus 7 | crawshaw | Builder runs on attached desktop, uses adb |
| darwin-amd64 | 2011 Mac Mini, 2.4Ghz Core i5 | adg       | Mac OS X 10.6 (10K549) |
| darwin-amd64-cheney | 2011 Mac Mini, 2.4Ghz Core i5 | Dave Cheney | Mac OS X 10.10 XCode 5 |
| darwin-amd64-race-cheney | 2011 Mac Mini, 2.4Ghz Core i5 | Dave Cheney | Mac OS X 10.10 XCode 5 |
| darwin-386 | 2011 Mac Mini, 2.4Ghz Core i5 | adg       | Mac OS X 10.6 (10K549) |
| darwin-386-cheney | 2011 Mac Mini, 2.4Ghz Core i5  | Dave Cheney | Mac OS X 10.10 XCode 5 |
| dragonfly-amd64 | ?               | Justin Sherrill | ?         |
| linux-arm-luitvd | RaspberryPi     | Luit van Drongelen |           |
| linux-arm-arm5 | QNAP TS-119P, ARMv5 @ 2.0GHz, 512MB | Dave Cheney | GOARM=5   |
| linux-arm-cheney-imx6 | Solidrun Cubox-i, quad core Cortex-A9 ~ 1Ghz, 2Gb ram | Dave Cheney | Runs arch linux, iMX6 boards need 3.10.x or above to pass the build reliably |
| linux-ppc64 | KVM instance on physical 8-core POWER7 pSeries. Chip rev: 2.1 (pvr 004b 0201) | bradfitz, rsc  |           |
| linux-ppc64-minux | Gentoo on PowerMac G5 (dual 2.7GHz ppc970fx) | minux  |           |
| nacl-arm  | samsung chromebook | rsc       | running chrubuntu |
| nacl-arm-cheney | same builder as linux-arm-cheney-imx6 | Dave Cheney |           |
| netbsd-386-minux | KVM             | minux |           |
| netbsd-amd64-bsiegert | EC2 m1.small VM | Benny Siegert | on Brad's work EC2 account |
| openbsd-arm | SolidRun CuBox-i4Pro, ARM Cortex A9 R2 792 MHz, 2GB RAM | Joel Sing |           |
| plan9-386-ducolombier | Intel Core 2 Quad Q8200 2.33 GHz, 6GB | David du Colombier | Plan 9 from Bell Labs, updated nightly |
| plan9-amd64-mischief | VM              | Nick Owens  | runs 9front |
| solaris-amd64-smartos | E5-1650 Xeon, 6C/12T | Daniel Malon | runs illumos (smartos zone); dfc, aram have full access |
| solaris-amd64-solaris11 | VM              | Dave Cheney | runs Solaris 11 |

# Builder Requirements
  * internet connection (at least be able to access Google and http://build.golang.org)
  * preferably with two or more (V)CPUs, as at least one test (` sync/atomic ` requires ` runtime.NumCPU() > 1 ` to test more completely)
  * at least 512MiB of memory

# Restrictions
  * The combination of Ubuntu 11.10 or 12.04 OMAP4 kernel and pandaboard (ES) have proven unstable as builders. See [issue 4305](https://code.google.com/p/go/issues/detail?id=4305). Make sure you have updated to the latest available 12.04.2 release.

# How to set up a builder
  1. obtain a hash from Go team members, and put that in ` ~/.gobuildkey `
  1. go get golang.org/x/build/cmd/builder
  1. builder YOUR\_BUILDER\_NAME

# Special notes
  * Please make sure you've installed root certificates and that it's accessible to Go programs. For example, on NetBSD, you will need to install ` security/mozilla-rootcerts `.
  * If your builder runs Unix, please install ` perl `, as tests for ` go.tools/cmd/vet ` need it.
  * Use ` screen(1) ` instead of ` tmux(1) ` to host the ` builder ` process, as the later interferes with some of the ` os/signal ` tests.
  * Raise ` ulimit `s on Unix: thread count (` -r `), nofiles (` -n `, 1024 should be fine)