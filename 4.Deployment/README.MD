## 4. Deployment
   
+ Pada tahap ini melakukan deploy aplikasi dengan menggunakan Docker Compose untuk command nya 'MYSQL_PASSWORD='<some password>' docker compose --file dist/docker-compose/docker-compose.yml up -d'  
+ Setelah itu melakukan implementasi Reverse Proxy dengan Nginx serta penggunaan SSL dari Cerbot dengan menggunakan domain 'https://retail.ahmad.studentdumbways.my.id/home'.
+ Selanjutnya, melakukan Push image dari Server aplikasi untuk disimpan di DockerHub.
+ Kemudian, melakukan percobaan akses ke domain aplikasi yang dibuat dan berhasil diakses di setiap halaman web aplikasi baik dari '/home', '/catalog' '/cart' dan '/checkout'
+ Berikut gambaran tahap pengerjaan Deployment:
