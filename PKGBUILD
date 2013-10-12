# Maintainer: Lance Chen <cyen0312+aur@gmail.com>

pkgbase=nova
pkgname=('nova-api'
         'nova-api-ec2'
         'nova-api-metadata'
         'nova-api-os-compute'
         'nova-baremetal'
         'nova-cells'
         'nova-cert'
         'nova-common'
         'nova-compute'
         'nova-compute-kvm'
         'nova-compute-lxc'
         'nova-compute-qemu'
         'nova-compute-uml'
         'nova-compute-xen'
         'nova-conductor'
         'nova-console'
         'nova-consoleauth'
         'nova-network'
         'nova-novncproxy'
         'nova-objectstore'
         'nova-scheduler'
         'nova-spiceproxy'
         'python2-nova')

pkgver=2013.2.rc2
pkgrel=1
pkgdesc="OpenStack Compute"
arch=(any)
url="https://launchpad.net/nova"
license=('Apache')
depends=('python2' 'python2-setuptools')
makedepends=('python2-setuptools')
install=nova.install
source=("$url/havana/havana-rc2/+download/$pkgbase-$pkgver.tar.gz"
        "nova-api-ec2.service"
        "nova-api-metadata.service"
        "nova-api-os-compute.service"
        "nova-api.service"
        "nova-baremetal.service"
        "nova-cells.service"
        "nova-cert.service"
        "nova-compute.conf"
        "nova-compute.service"
        "nova-conductor.service"
        "nova-console.service"
        "nova-consoleauth.service"
        "nova-network.service"
        "nova-novncproxy.service"
        "nova-objectstorage.service"
        "nova-scheduler.service"
        "nova-spiceproxy.service"
        "nova.tmpfiles"
        "nova_sudoers")
md5sums=('3b8c2888799d12d862b96db187972036'
         '5f6a51b82bd293e2d854e2b5917dcd6c'
         '755796774821221622f09e600a0364b1'
         '3915c4fd03128a730ef08293c9010d7a'
         '3626a061e8b2399d144fa5be1d05e552'
         'e1762c4431d8abcfe1ad167e172ad858'
         '7cd1d470fcf8c6ecd77b4d521406c50f'
         'fe73717f98598f5640e23d15a672bde4'
         'e5c43117a259feef7120847441a776a5'
         'a45e6fd8b0580e92064b7bba9ef1df79'
         'c3a88bc9eb2ab808875cd79efdde6889'
         'bcfa4451076ee180ee867376065a13fc'
         '0d700761b08baae4e550276eb06e4910'
         '62d823032a8d5de920b46897174ef58b'
         '28f21415803757a408a6883fa53b40fc'
         '22b40866dfba304ce187cf2185ea82e7'
         '956e928f7242a17544e4e1dbde3cacf9'
         'e68d9e2895b8616aa35e4e4f2e807070'
         '27e809e427394f823cbc48cac3119a28'
         '539ce3151b597b066cb0e31e0a731b54')

build() {
  cd "$pkgbase-$pkgver"
  /usr/bin/python2 setup.py build
  /usr/bin/python2 setup.py install --root="$srcdir/tmp" \
                           --install-data="/" \
                           --optimize=1
  cp -R etc/ $srcdir/tmp/
}

package_nova-api() {
  pkgdesc+=" - API frontend"
  depends=('iptables' 'nova-common')

  cd tmp

  install -D -m 644 etc/nova/rootwrap.d/api-metadata.filters \
                    ${pkgdir}/etc/nova/rootwrap.d/api-metadata.filters
  install -D -m 755 usr/bin/nova-api ${pkgdir}/usr/bin/nova-api
  install -D -m 644 ${srcdir}/nova-api.service ${pkgdir}/usr/lib/systemd/system/nova-api.service
}

package_nova-api-ec2() {
  pkgdesc+=" - EC2 API frontend"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-api-ec2 ${pkgdir}/usr/bin/nova-api-ec2
  install -D -m 644 ${srcdir}/nova-api-ec2.service ${pkgdir}/usr/lib/systemd/system/nova-api-ec2.service
}

package_nova-api-metadata() {
  pkgdesc+=" - metadata API frontend"
  depends=('nova-common')

  cd tmp

  install -D -m 644 etc/nova/rootwrap.d/api-metadata.filters \
                    ${pkgdir}/etc/nova/rootwrap.d/api-metadata.filters
  install -D -m 755 usr/bin/nova-api-metadata ${pkgdir}/usr/bin/nova-api-metadata
  install -D -m 644 ${srcdir}/nova-api-metadata.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-api-meatadata.service
}

package_nova-api-os-compute() {
  pkgdesc+=" - Compute API frontend"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-api-os-compute ${pkgdir}/usr/bin/nova-api-os-compute
  install -D -m 644 ${srcdir}/nova-api-os-compute.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-api-os-compute.service
}

package_nova-baremetal() {
  pkgdesc+=" - baremetal virt"
  depends=('nova-common')

  cd tmp

  install -d ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-baremetal-deploy-helper ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-baremetal-manage ${pkgdir}/usr/bin/

  install -D -m 644 ${srcdir}/nova-baremetal.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-baremetal.service
}

package_nova-cells() {
  pkgdesc+=" - cells"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-cells ${pkgdir}/usr/bin/nova-cells
  install -D -m 644 ${srcdir}/nova-cells.service ${pkgdir}/usr/lib/systemd/system/nova-cells.service
}

package_nova-cert() {
  pkgdesc+=" - certificate management"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-cert ${pkgdir}/usr/bin/nova-cert
  install -D -m 644 ${srcdir}/nova-cert.service ${pkgdir}/usr/lib/systemd/system/nova-cert.service
}

package_nova-common() {
  pkgdesc+=" - common"
  depends=('python2-nova')
  backup=('etc/nova/nova.conf'
          'etc/nova/api-paste.ini')

  cd tmp

  install -d ${pkgdir}/etc/nova/
  install -m 640 etc/nova/api-paste.ini ${pkgdir}/etc/nova/
  install -m 644 etc/nova/logging_sample.conf ${pkgdir}/etc/nova/logging.conf
  install -m 640 etc/nova/policy.json ${pkgdir}/etc/nova/
  install -m 640 etc/nova/nova.conf.sample ${pkgdir}/etc/nova/nova.conf
  install -m 644 etc/nova/rootwrap.conf ${pkgdir}/etc/nova/
  
  install -d ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-manage ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-rootwrap ${pkgdir}/usr/bin/

  install -d -m 0750 ${pkgdir}/etc/sudoers.d/
  install -m 440 ${srcdir}/nova_sudoers ${pkgdir}/etc/sudoers.d/

  install -D -m 644 ${srcdir}/nova.tmpfiles ${pkgdir}/usr/lib/tmpfiles.d/nova.conf

  install -d -m 0770 ${pkgdir}/run/lock/nova/
  install -d -m 0770 ${pkgdir}/var/lib/nova/
  install -d -m 0770 ${pkgdir}/var/log/nova/
}

package_nova-compute() {
  pkgdesc+=" - compute node"
  depends=('curl'
           'ebtables'
           'gawk'
           'iptables'
           'lsb-release'
           'nova-common'
           'open-iscsi'
           'parted')

  cd tmp

  install -D -m 644 etc/nova/rootwrap.d/compute.filters ${pkgdir}/etc/nova/rootwrap.d/compute.filters
  install -D -m 755 usr/bin/nova-compute ${pkgdir}/usr/bin/nova-compute
  install -D -m 644 ${srcdir}/nova-compute.service ${pkgdir}/usr/lib/systemd/system/nova-compute.service
}

package_nova-compute-kvm() {
  pkgdesc+=" - compute node (KVM)"
  depends=('libvirt'
           'nova-compute'
           'qemu')
  provides=('nova-compute-hypervisor')
  backup=('etc/nova/nova-compute.conf')

  cd tmp

  install -D -m 644 ${srcdir}/nova-compute.conf ${pkgdir}/etc/nova/nova-compute.conf
  sed -i s/libvirt_type\=.*$/libvirt_type\=kvm/ ${pkgdir}/etc/nova/nova-compute.conf
}

package_nova-compute-lxc() {
  pkgdesc+=" - compute node (LXC)"
  depends=('libvirt'
           'nova-compute')
  provides=('nova-compute-hypervisor')
  backup=('etc/nova/nova-compute.conf')

  cd tmp

  install -D -m 644 ${srcdir}/nova-compute.conf ${pkgdir}/etc/nova/nova-compute.conf
  sed -i s/libvirt_type\=.*$/libvirt_type\=lxc/ ${pkgdir}/etc/nova/nova-compute.conf
}

package_nova-compute-qemu() {
  pkgdesc+=" - compute node (QEmu)"
  depends=('libvirt'
           'nova-compute'
           'qemu')
  provides=('nova-compute-hypervisor')
  backup=('etc/nova/nova-compute.conf')

  cd tmp

  install -D -m 644 ${srcdir}/nova-compute.conf ${pkgdir}/etc/nova/nova-compute.conf
  sed -i s/libvirt_type\=.*$/libvirt_type\=qemu/ ${pkgdir}/etc/nova/nova-compute.conf
}

package_nova-compute-uml() {
  pkgdesc+=" - compute node (UserModeLinux)"
  depends=('libvirt'
           'nova-compute'
           'linux-usermode')
  provides=('nova-compute-hypervisor')
  backup=('etc/nova/nova-compute.conf')

  cd tmp

  install -D -m 644 ${srcdir}/nova-compute.conf ${pkgdir}/etc/nova/nova-compute.conf
  sed -i s/libvirt_type\=.*$/libvirt_type\=uml/ ${pkgdir}/etc/nova/nova-compute.conf
}

package_nova-compute-xen() {
  pkgdesc+=" - compute node (Xen)"
  depends=('libvirt'
           'nova-compute'
           'xen-4.3-git')
  provides=('nova-compute-hypervisor')
  backup=('etc/nova/nova-compute.conf')

  cd tmp

  install -D -m 644 ${srcdir}/nova-compute.conf ${pkgdir}/etc/nova/nova-compute.conf
  sed -i s/libvirt_type\=.*$/libvirt_type\=xen/ ${pkgdir}/etc/nova/nova-compute.conf
}

package_nova-conductor() {
  pkgdesc+=" - conductor service"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-conductor ${pkgdir}/usr/bin/nova-conductor
  install -D -m 644 ${srcdir}/nova-conductor.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-conductor.service
}

package_nova-console() {
  pkgdesc+=" - Console"
  depends=('nova-common')
  optdepends=('nova-consoleauth')

  cd tmp

  install -D -m 755 usr/bin/nova-console ${pkgdir}/usr/bin/nova-console
  install -D -m 644 ${srcdir}/nova-console.service ${pkgdir}/usr/lib/systemd/system/nova-console.service
}

package_nova-consoleauth() {
  pkgdesc+=" - Console Authenticator"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-consoleauth ${pkgdir}/usr/bin/nova-consoleauth
  install -D -m 644 ${srcdir}/nova-consoleauth.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-consoleauth.service
}

package_nova-network() {
  pkgdesc+=" - Network manager"
  depends=('bridge-utils'
           'dnsmasq'
           'iptables'
           'iputils'
           'netcat'
           'nova-common')
  optdepends=('radvd')

  cd tmp

  install -D -m 644 etc/nova/rootwrap.d/network.filters ${pkgdir}/etc/nova/rootwrap.d/network.filters

  install -d ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-dhcpbridge ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-network ${pkgdir}/usr/bin/

  install -D -m 644 ${srcdir}/nova-network.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-network.service
}

package_nova-novncproxy() {
  pkgdesc+=" - NoVNC proxy"
  depends=('nova-common'
           'novnc'
           'websockify')

  cd tmp

  install -D -m 755 usr/bin/nova-novncproxy ${pkgdir}/usr/bin/nova-novncproxy
  install -D -m 644 ${srcdir}/nova-novncproxy.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-novncproxy.service
}

package_nova-objectstore() {
  pkgdesc+=" - object store"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-objectstore ${pkgdir}/usr/bin/nova-objectstore
  install -D -m 644 ${srcdir}/nova-objectstorage.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-objectstorage.service
}

package_nova-scheduler() {
  pkgdesc+=" - virtual machine scheduler"
  depends=('nova-common')

  cd tmp

  install -d ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-clear-rabbit-queues ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-rpc-zmq-receiver ${pkgdir}/usr/bin/
  install -m 755 usr/bin/nova-scheduler ${pkgdir}/usr/bin/

  install -D -m 644 ${srcdir}/nova-scheduler.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-scheduler.service
}

package_nova-spiceproxy() {
  pkgdesc+=" - spice html5 proxy"
  depends=('nova-common')

  cd tmp

  install -D -m 755 usr/bin/nova-spicehtml5proxy ${pkgdir}/usr/bin/nova-spicehtml5proxy
  install -D -m 644 ${srcdir}/nova-spiceproxy.service \
                    ${pkgdir}/usr/lib/systemd/system/nova-spiceproxy.service
}

package_python2-nova() {
  pkgdesc+=" - Python library"
  depends=('openssh' 
           'openssl'
           'python2-amqplib>=0.6.1'
           'python2-anyjson>=0.3.3'
           'python2-babel>=0.9.6'
           'python2-boto>=2.4.0'
           'python2-cinderclient>=1.0.5'
           'python2-eventlet>=0.13.0'
           'python2-glanceclient>=0.9.0'
           'python2-greenlet>=0.3.2'
           'python2-iso8601>=0.1.4'
           'python2-jinja'
           'python2-jsonschema>=1.3.0'
           'python2-keystoneclient>=0.3.2'
           'python2-kombu>=2.4.8'
           'python2-lxml>=2.3'
           'python2-migrate>=0.7.2'
           'python2-neutronclient>=2.3.0'
           'python2-neutronclient<3.0.0'
           'python2-oslo-config>=1.2.0'
           'python2-paramiko>=1.8.0'
           'python2-paste'
           'python2-paste-deploy>=1.5.0'
           'python2-pbr>=0.5.21'
           'python2-pbr<1.0.0'
           'python2-pyasn1'
           'python2-routes>=1.12.3'
           'python2-six<1.4.0'
           'python2-sqlalchemy-0.7.9'
           'python2-stevedore>=0.10'
           'python2-suds>=0.4'
           'python2-webob>=1.2.3'
           'python2-webob<1.3.0'
           'sudo'
           'websockify>=0.5.1'
           'websockify<0.6')
  optdepends=('mysql-python')

  cd tmp

  install -d ${pkgdir}/usr/lib/
  cp -R usr/lib/ ${pkgdir}/usr/
}

# vim:set ts=2 sw=2 et:
