# 🌐オンラインチャットサービス💬  

## 📌 目次
**このドキュメントの目次です。各セクションへジャンプできます。**

<hr style="border: 3px solid black;">

## **📎 概要**
- [概要](#概要)
- [シミュレーション](#シミュレーション)
- [実行方法](#実行方法)

---

## **🛠 技術関連**
- [使用技術](#使用技術)
- [機能一覧](#機能一覧)

---

## **📍開発のポイント**
- [こだわりのポイント](#こだわりのポイント)
- [苦労した点](#苦労した点)
- [さらに追加したい機能](#さらに追加したい機能)

---

## **📄 参考情報**
- [参考文献](#参考文献)

---

## 🍀 概要
ユーザがルームを作成または参加して、グループチャットができるサービス

## 🖥 シミュレーション

## ▶️ 実行方法

## 🛠 使用技術

| カテゴリ | 技術スタック |
|----------|------------|
| 開発言語 | Python 3.13.2 |
| インフラ | Docker |
| その他 | Git, GitHub |


## ⚙ 機能一覧

## ✨ こだわりのポイント

## ⚠️ 苦労した点

## 💡 さらに追加したい機能

## 📄 参考文献



## 1. server.pyのクラス図
```mermaid
classDiagram
    direction LR

    TCPServer -- UDPServer

    class TCPServer {
        -HEADER_MAX_BYTE: int
        -TOKEN_MAX_BYTE: int
        -server_address: str
        -server_port: int
        -sock: socket
        -room_members_map: dict
        -clients_map: dict
        +__init__(server_address: str, server_port: int)
        +start_tcp_server(): None
        -accept_tcp_connections(): None
        -handle_client_request(connection: socket, client_address: tuple): None
        -decode_message(data: bytes): tuple
        -register_client(token: bytes, client_address: tuple, room_name: str, payload: str, operation: int): None
        -create_room(connection: socket, room_name: str, payload: str, token: bytes): None
        -join_room(connection: socket, room_name: str, payload: str, token: bytes): None
    }

    class UDPServer {
        -server_address: str
        -server_port: int
        -room_members_map: dict
        -clients_map: dict
        -sock: socket
        +__init__(server_address: str, server_port: int)
        +start_udp_server(): None
        -handle_messages(): None
        -decode_message(data: bytes): tuple
        -broadcast_message(room_name: str, message: str): None
        -remove_inactive_clients(): None
        -disconnect_inactive_client(client_token: bytes, client_info: list): None
    }
```
## 2. client.pyのクラス図
```mermaid
classDiagram
    direction LR

    TCPClient -- UDPClient

    class TCPClient {
        -server_address: str
        -server_port: int
        -sock: socket
        -client_info: dict
        +__init__(server_address: str, server_port: int)
        +start_tcp_client(): dict
        -connect_to_server(): None
        -input_user_name(): str
        -input_operation(): int
        -create_room(username: str): tuple
        -input_room_name(operation: int): str
        -create_packet(room_name: str, operation: int, state: int, payload: str): bytes
        -create_header(room_name: str, operation: int, state: int, payload: str): bytes
        -join_room(username: str): tuple
    }

    class UDPClient {
        -server_address: str
        -server_port: int
        -sock: socket
        -my_info: dict
        -my_token: bytes
        -room_name: str
        +__init__(server_address: str, server_port: int, my_info: dict)
        +start_udp_chat(): None
        -send_username(): None
        -send_message(): None
        -receive_message(): None
        -create_packet(message: bytes = b""): bytes
    }

```
