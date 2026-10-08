## IP Address Classes

Summary of IPv4 address classes based on their first octet binary structure and numeric range.

## Class Breakdown

| Class | First Octet (Binary) | First Octet Numeric Range |
| :---: | :------------------- | :------------------------ |
| **A** | `0xxxxxxx`           | 0 - 127                   |
| **B** | `10xxxxxx`           | 128 - 191                 |
| **C** | `110xxxxx`           | 192 - 223                 |
| **D** | `1110xxxx`           | 224 - 239                 |
| **E** | `1111xxxx`           | 240 - 255                 |

- **Class A-C:** Used for **unicast** addressing in standard networks.
- **Class D:** Reserved for **multicast** routing.
- **Class E:** Reserved for **experimental** and research purposes.

- If an IP address belongs to the **127.x.x.x network range**, those are called loopback addresses. These addresses are used for defining local hosts and are usually used for checking if the TCP/IP stack works properly.

- To calculate the maximum number of the hosts per Network:
For network address **x.x.x.x/n** the maximum number of hosts is calculated as follows: $$ 2^n - 2$$
