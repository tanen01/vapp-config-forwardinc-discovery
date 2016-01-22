# vapp-config-discovery-forwardinc

===================================

This config monitors dsa PODs and updates etcd with information that are
required by the dxgrid sidecar to configure dxgrid.

DSA information are inserted as entries under the /dsas/ subtree in etcd.
Each entry's key is an integer from 0..n, where n is the number of dxgrid replicas.

For example, if there are 2 replicas then the entries under /dsas/ would look like:

```
{
  "action": "get",
  "node": {
    "key": "/dsas",
    "dir": true,
    "nodes": [
      {
        "key": "/dsas/0",
        "value": "dxgrid-data-rc-ylgiq/10.244.85.6",
        "modifiedIndex": 40,
        "createdIndex": 40
      },
      {
        "key": "/dsas/1",
        "value": "dxgrid-data-rc-u1per/10.244.83.6",
        "modifiedIndex": 41,
        "createdIndex": 41
      }
    ],
    "modifiedIndex": 3,
    "createdIndex": 3
  }
}
```

Lets look at the first entry:
  - "value"  has 2 pieces of information -- The POD's hostname and IP separated by a forward slash
    character. In this example, the POD's hostname is "dxgrid-data-rc-ylgiq" and IP is
    "dxgrid-data-rc-ylgiq"
  - "key" is a number that will be used as the "DSA number". DSA name follows the format
    dsa[DSA number]. In this example, the first DSA is named "dsa0" and the second "dsa1".