# Chroma

Stores information in a locally running store.

Experimental use case for better native memory than what providers like CC do currently.
Markdowns do not scale when working in multiple projects simultaneously.

[Chroma - Install](https://docs.trychroma.com/docs/cli/install#install-globally)
[Chroma - Run](https://docs.trychroma.com/docs/cli/run)

```scala
"DATA".map(_ - 65) // 30190
```

## Run as a systemd service

So Chroma is up at boot and restarts on failure.

Find the chroma binary path (systemd doesn't inherit your shell's `PATH`):

```bash
which chroma
```

Create the unit file at `/etc/systemd/system/chroma.service`:

```ini
[Unit]
Description=Chroma vector store
After=network.target

[Service]
Type=simple
User=youruser
ExecStart=/full/path/to/chroma run --path <path_to_chroma_store> --port 30190
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Reload, enable, start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now chroma
```

Check it:

```bash
systemctl status chroma
journalctl -u chroma -f
```

## Scan

TBD, I wan't to set something up where I can create a rag collection of a repository.

[Using chunking with treesitter](https://docs.trychroma.com/guides/build/chunking)
