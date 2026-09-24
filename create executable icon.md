
-  sudo mv ~/Downloads/Postman /opt/Postman
- sudo nano /usr/share/applications/postman.desktop
```
[Desktop Entry]
Name=Postman
Comment=API Development Environment
Exec=/opt/Postman/Postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;Utility;
```
- sudo chmod +x /usr/share/applications/postman.desktop
-  sudo update-desktop-database