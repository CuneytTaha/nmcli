nmcli
=====

nmcli is a python wrapper library for the network-manager cli client.

## Quick Sample

Here is a simple usecase.

```python
import nmcli

try:
    print(nmcli.connection())
    print(nmcli.device())
    print(nmcli.device.wifi())
    print(nmcli.general())

    nmcli.device.wifi_connect('AP1', 'passphrase')
    nmcli.connection.modify('AP1', {
            'ipv4.addresses': '192.168.1.1/24',
            'ipv4.gateway': '192.168.1.255',
            'ipv4.method': 'manual'
        })
    nmcli.connection.down('AP1')
    nmcli.connection.up('AP1')
    nmcli.connection.delete('AP1')
except Exception as e:
    print(e)
```

## Dependency

* NetworkManager
  * `sudo apt install network-manager` (Debian)
* User who can execute nmcli with sudo with NOPASSWD

## API

### `nmcli.connection`

Get a list of connections.

```python
nmcli.connection() -> List[Connection]
```

### `nmcli.connection.add`

Create a new connection using specified properties.

```python
nmcli.connection.add(
    conn_type: str,
    options: Optional[Dict[str, str]] = None,
    ifname: str = "*",
    name: str = None,
    autoconnect: bool = False) -> None
```

### `nmcli.connection.modify`

Add, modify or remove properties in the connection profile.

```python
nmcli.connection.modify(name: str, options: Dict[str, str]) -> None
```

### `nmcli.connection.delete`

Delete a configured connection.

```python
nmcli.connection.delete(name: str) -> None
```

### `nmcli.connection.up`

Activate a connection.

```python
nmcli.connection.up(name: str) -> None
```

### `nmcli.connection.down`

Deactivate a connection from a device without preventing the device from further auto-activation.

```python
nmcli.connection.down(name: str) -> None
```

## Change Log

### 0.1.0

Initial release.

## License

MIT
