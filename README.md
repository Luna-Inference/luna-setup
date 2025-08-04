# luna-setup
A set of instructions to setup luna - absolutely required

# SSL
# Generate private key (2048-bit RSA)
openssl genrsa -out luna.key 2048

# Generate self-signed certificate valid for 100 years (36500 days)
openssl req -new -x509 -key luna.key -out luna.crt -days 36500 \
    -subj "/C=US/ST=CA/L=SF/O=Luna/CN=169.254.200.100" \
    -addext "subjectAltName=IP:169.254.200.100,DNS:luna.local"

# Set proper permissions
chmod 600 luna.key
chmod 644 luna.crt