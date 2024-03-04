## 4. Deployment
   
+ Pada tahap ini melakukan deploy aplikasi dengan menggunakan Docker Compose untuk command nya `MYSQL_PASSWORD='<some password>' docker compose --file dist/docker-compose/docker-compose.yml up -d`  
+ Setelah itu melakukan implementasi Reverse Proxy dengan Nginx serta penggunaan SSL dari Cerbot dengan menggunakan domain `https://retail.ahmad.studentdumbways.my.id/home`.
+ Selanjutnya, melakukan Push image dari Server aplikasi untuk disimpan di DockerHub.
+ Kemudian, melakukan percobaan akses ke domain aplikasi yang dibuat dan berhasil diakses di setiap halaman web aplikasi baik dari `/home`, `/catalog` `/cart` dan `/checkout`
+ Berikut gambaran tahap pengerjaan Deployment:

![Screenshot from 2024-03-04 18-03-19](https://github.com/Muna-020/Test-DevOps/assets/74352384/46ed7dea-b27b-41e4-8fff-511531393a6d)

![Screenshot from 2024-03-04 18-03-24](https://github.com/Muna-020/Test-DevOps/assets/74352384/61e1cdfb-c24a-4313-9676-a30c43192b3d)

![Screenshot from 2024-03-04 18-03-59](https://github.com/Muna-020/Test-DevOps/assets/74352384/c4d4b1fc-8a91-44bb-b12f-48b0be9c73d2)

![Screenshot from 2024-03-04 18-03-51](https://github.com/Muna-020/Test-DevOps/assets/74352384/4380d0eb-e71f-445f-8571-5156b0c5abf6)

![Screenshot from 2024-03-04 18-04-30](https://github.com/Muna-020/Test-DevOps/assets/74352384/b4458845-ff5c-4853-87b8-7d969f16b583)
