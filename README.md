# Installation Procedure

## 1. Install IPBus (uHAL/controlHub)

Follow the official guide:  
[https://ipbus.web.cern.ch/doc/user/html/software/index.html](https://ipbus.web.cern.ch/doc/user/html/software/index.html)  
If your OS is Ubuntu, 
```bash
sudo apt-get install -y make erlang g++ libboost-all-dev libpugixml-dev python-all-dev rsyslog
sudo touch /usr/lib/erlang/man/man1/x86_64-linux-gnu-gcov-tool.1.gz
sudo touch /usr/lib/erlang/man/man1/gcov-tool.1.gz
git clone --depth=1 -b v2.8.17 --recurse-submodules https://github.com/ipbus/ipbus-software.git
cd ipbus-software
make 
(sudo make install)
```

During the `make` process, you may encounter the issue described in:  
[GitHub Issue #310](https://github.com/ipbus/ipbus-software/issues/310#issuecomment-2202467383)

To fix this, modify `controlhub/rebar.config` as follows:

```erlang
{deps, [
  {lager, "3.9.2", {git, "https://github.com/erlang-lager/lager.git", {tag, "3.9.2"}}},
  {syslog, "1.0.5", {git, "https://github.com/Vagabond/erlang-syslog.git", {tag, "1.0.5"}}},
  {lager_syslog, "2.1.2", {git, "https://github.com/erlang-lager/lager_syslog.git", {tag, "3.0.3"}}}
]}.
```

Then run:

```bash
make clean
make
sudo make install
```
## 2. Install cURL
```bash
# Ubuntu/Debian
sudo apt-get install libcurl4-openssl-dev

# CentOS/RHEL
sudo yum install libcurl-devel
# or
sudo dnf install libcurl-devel
```
## 3. Set Environment Variables

Add the following lines to your `~/.bashrc` or `~/.zshrc`:

```bash
export LD_LIBRARY_PATH=/opt/cactus/lib:$LD_LIBRARY_PATH
export PATH=/usr/bin/:/opt/cactus/bin:$PATH
```

Then source the shell configuration:

```bash
source ~/.bashrc
```

## 4. Clone and Build AIDATLU

Clone the repository:

```bash
git clone https://github.com/eyiliu/aidatlu.git
cd aidatlu
```

Create and enter the build directory:

```bash
mkdir build
cd build
```

Run CMake (you may need to install it with `sudo apt-get install cmake`):

```bash
cmake ../
```

Build and install:

```bash
make -j8 install
```

## 5. Final Checks

Verify the installation:

```bash
/opt/cactus/bin/controlhub_start
./INSTALL/bin/aidatluTool
```

---

