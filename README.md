# ITE183 Laboratory 2: WebSocket Server

An event-driven, multi-client chat server written in Bonezegei Scripting Language (BSL). It serves a browser chat interface over HTTP and broadcasts messages between connected WebSocket clients.

## Project Structure

```text
.
|-- app.bzg            # HTTP and WebSocket server
|-- package.json       # BSL package metadata and http dependency
|-- public/
|   |-- index.html     # Real-time chat client
|   `-- 404.html       # Page for unknown routes
|-- documentation/     # Screenshot evidence
|-- .gitattributes
|-- .gitignore
`-- LICENSE
```

`lib/` is created by `bzg install` and is not committed.

## Requirements

- Bonezegei v1.3.3


- BSL package manager (`bzg`)
- A browser with WebSocket support


Verify the version:

```powershell
bonezegei -v


`

## Install and Run

From the project root:

```powershell
bzg install
bzg run
```

The server listens on port `8000`. Open <http://localhost:8000/> in two or more browser windows and send messages; each window shows messages from all clients. Visit any other path (for example `/anything`) to see the custom 404 page. The terminal logs connect, message, and disconnect events. Stop the server with `Ctrl+C`.

## Windows Troubleshooting Note

On this Windows machine, `bzg run` first failed with `Failed to load library: lib/http/http.dll` (Win32 error 126), because `http.dll` depends on `libwinpthread-1.dll`, which was not installed. Copying a 64-bit copy of that file (from Git's `mingw64\bin` folder) into `lib\http\` fixed it. The DLL is not committed to this repository.

## Routes and WebSocket Events

| Request | Behavior |
| --- | --- |
| `/` or `/index.html` | Serves `public/index.html` |
| Any other path | Serves `public/404.html` |
| WebSocket connect | Logs the client ID and sends a welcome message |
| WebSocket message | Broadcasts `User <clientId> says: <message>` to all clients |
| WebSocket disconnect | Logs the client ID |

## Screenshot Evidence

Saved in `documentation/`:

- `01-version.png`: `bonezegei -v` showing v1.3.3
- `02-bzg-install.png`: `bzg install` output
- `03-server-start.png`: server started with `bzg run`
- `04-multi-client-chat.png`: two browser clients showing broadcast messages
- `05-404-page.png`: custom 404 page

## License

MIT License. See [LICENSE](LICENSE).