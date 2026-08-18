https://raw.githubusercontent.com/AngelGonePro/jellyfin-docker/refs/heads/main/jellyfin.zip
```
mkdir ~/jellyfin && \
wget -O /tmp/jellyfin.zip https://raw.githubusercontent.com/AngelGonePro/jellyfin-docker/refs/heads/main/jellyfin.zip && \
python3 - << 'EOF'
import zipfile, os

zip_path = "/tmp/jellyfin.zip"
extract_to = "jellyfin"

with zipfile.ZipFile(zip_path) as z:
    for member in z.namelist():
        parts = member.split("/", 1)
        if len(parts) > 1:
            target = os.path.join(extract_to, parts[1])
            if not member.endswith("/"):
                os.makedirs(os.path.dirname(target), exist_ok=True)
                with open(target, "wb") as f:
                    f.write(z.read(member))
EOF
rm /tmp/jellyfin.zip
```
