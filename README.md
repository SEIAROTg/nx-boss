# nx-boss

Compatible server for PaperStream NX Manager.

This allows compatible scanners (e.g. fi-7300NX) to scan directly over network, with NO driver, NO Windows, NO USB, NO proprietary software.

## Usage

```console
$ pip install git+https://github.com/SEIAROTg/nix-boss.git
$ curl -OL https://github.com/SEIAROTg/nx-boss/raw/refs/heads/main/config.example.yaml
$ mkdir out  # `output_path` in config
$ python -m nx_boss -c config.example.yaml --host 0.0.0.0 --port 10447
```

Connect your scanner to server and happy scanning!

## HTTPS

To encrypt traffic between the scanner and the server, pass a certificate and key:

```console
$ openssl req -x509 -newkey rsa:2048 -sha256 -nodes -days 7300 -keyout key.pem -out cert.pem \
    -subj /CN=<server-ip> -addext subjectAltName=IP:<server-ip>
$ python -m nx_boss -c config.example.yaml --host 0.0.0.0 --port 20447 --ssl-certfile cert.pem --ssl-keyfile key.pem
```

Then turn on encryption in the scanner's PaperStream NX Manager settings and use port 20447. Tested on a fi-7300NX, which accepts a self-signed certificate.

## Note

- ⚠️ Use at your own risk. The authors are not responsible for any damage.
- Check [code](./src/nx_boss/__main__.py) for a complete list of settings.
- This is not subject to the 400dpi limit in PaperStream NX Manager.
- This is not designed for enterprise use and thus does not include features like authentication, per-scanner job group, log, email, s3, etc., but they should be trivial to implement.
