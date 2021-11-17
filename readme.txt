# mostly taken from: https://github.com/Maccraft123/Cadmium/commit/3568ee7dd9c1f5c550129753b491bbfe4214b15f

mkdir -p /compile/source/qcom-tools/
cd /compile/source/qcom-tools/
git clone https://github.com/andersson/qmic
git clone https://github.com/andersson/qrtr
git clone https://github.com/Maccraft123/rmtfs

cd qmic
make prefix=/usr clean
make prefix=/usr install
cd ../qrtr
make prefix=/usr clean
make prefix=/usr install
cd ../rmtfs
make prefix=/usr clean
make prefix=/usr install

mkdir -p /lib/firmware/rmtfs
dd if=/dev/zero bs=1M count=2 of=/lib/firmware/rmtfs/modem_fs1
dd if=/dev/zero bs=1M count=2 of=/lib/firmware/rmtfs/modem_fs2
dd if=/dev/zero bs=1M count=2 of=/lib/firmware/rmtfs/modem_fsg
dd if=/dev/zero bs=1M count=2 of=/lib/firmware/rmtfs/modem_fsc

tar czf /tmp/qcom-tools.tar.gz /usr/bin/qmic /usr/bin/qrtr-ns /usr/bin/qrtr-cfg /usr/bin/qrtr-lookup /usr/bin/rmtfs /usr/lib/libqrtr.so.1.0 /usr/lib/libqrtr.so.1 /usr/lib/libqrtr.so /usr/lib/systemd/system/qrtr-ns.service /usr/lib/systemd/system/rmtfs.service /usr/include/libqrtr.h /lib/firmware/rmtfs/modem_fs1 /lib/firmware/rmtfs/modem_fs2 /lib/firmware/rmtfs/modem_fsg /lib/firmware/rmtfs/modem_fsc
