# yamt-boshrelease
BOSH release containing yamt (see https://github.com/bo0mer/yamt)

## Usage
This release is not intended for stand-alone usage. It is rather useful for composing the jobs with your own release jobs in order to get your desired metrics in Riemann.

## Jobs
The release has the following jobs:
* yamt

### yamt
ATM The job collects only network interface metrics from the VM and emits them to Riemann. It does so by reading from `/proc/net/dev`.

List of metrics that are collected and emitted for each specified interface:

* `bytes` - The total number of bytes of data transmitted or received by the interface.
* `packets`- The total number of packets of data transmitted or received by the interface.
* `errs` - The total number of transmit or receive errors detected by the device driver.
* `drop` - The total number of packets dropped by the device driver.
* `fifo` - The number of FIFO buffer errors.
* `frame` - The number of packet framing errors.
* `colls` - The number of collisions detected on the interface.
* `compressed` - The number of compressed packets transmitted or received by the device driver.
* `carrier` - The number of carrier losses detected by the device driver.
* `multicast` - The number of multicast frames transmitted or received by the device driver.

:rotating_light: Note that this metrics are reported both for receive and transmit.

#### Available configuration

ATM it is possible to exclude a interface so that its metrics won't be emitted. That is done by adding it to the `yamt.ignore_interfaces` property. Following is a list of all supported configuration properties.

```
yamt.host:
  description: "Address of the Riemann server to report to."
yamt.port:
  description: "Port of the Riemann server to report to."
  default: 5555
yamt.interval:
  description: "Interval between reports (in seconds)."
  default: 5
yamt.ignore_interfaces:
  description: "Interfaces to ignore."
  default: "lo"
```
