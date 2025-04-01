# UNOFFICIAL Skyter IPTVAPI docs

## Info
This documentation is based of requests from the LBOX IPTV client captured by WireShark. Since these are not encrypted, so it's quite easy to reverse engineer. I don't know if these requests are different per provider, so take this with a grain of salt.

All these requests were captured from a device tied to VdaliTV. These requests may differ between different providers.

## Authentication
### Login
```
GET /iptv/api/v1/json/login
```
#### URL parameters
- `login` -> a string of numbers (e.g. `283929`)
- `pass` -> a string of characters from `1` to `f` (e.g. `2837787a8b87c878f8798e9899a89d98`)
- `with_acc` -> is set to `1` with my box, not sure what it does
- `with_cfg` -> is set to `1` with my box, not sure what it does
- `torrent` -> changes server behavior (default 2)
  - `0` -> disables torrents
  - `2` -> enables torrents
#### Response format
```
{
    "sid": "[session id]",
    "version": "1.0",
    "account": {
        "id": "[login]",
        "title": "[title set by provider]",
        "balance": "0.0000",
        "acc_level": "1",
        "node_id": "1",
        "subscriptions": [
            {
                "title": "[title of subscription]",
                "contents_type": "0",
                "option": "11100001",
                "continuous": "1",
                "begin_date": "1970-01-01",
                "type_id": "1",
                "type_ru": "[type of subscription in russian]",
                "type_en": "[type of subscription]",
                "end_date": "1970-01-01",
                "rest_of_days": "0"
            },
            ...
        ]
    },
    "settings": {
        "time_zone": 60,
        "time_shift": 0,
        "interface_lng": "en",
        "parental_pass": 1111,
        "media_server_id": 1,
        "stb_volume": 60,
        "stb_bright": 65,
        "stb_contrast": 50,
        "stb_saturation": 50,
        "stb_buffer": 5,
        "media_servers": [
            {
                "id": "1",
                "title": "[title of server]"
            },
            ...
        ]
    },
    "servertime": 0
}
```
<sub>Note: I do not know what some of these do (e.g. options). I just return them as is without modification and it works.</sub>
