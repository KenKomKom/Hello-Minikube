![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/a44c29d8-fcbf-4a4c-9404-ac8684e7d6a1)### Hello-Minikube
1. Compare the application logs before and after you exposed it as a Service.

   Ya, terdapat perbedaan karena setelah service di expose. Service dapat menerima request sehingga pada log akan tercatat request-request yang pernah terbuat, misal seperti berikut jika dilakukan refresh berkali-kali terhadap service hello-node.
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/8652396e-de55-48b6-84d3-0b44a0636afb)
2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to
`kube-system`.

  Perbedaan dari kedua syntax tersebut adalah dengan menggunakan -n, kita menyatakan kalau service yang kita mau adalah dari yang berada pada namespace tersebut. Hal ini diperlukan jika misal terdapat banyak service berbeda yang memiliki nama yang sama dan tersebar di banyak namespace. Dengan menggunakan -n, kita memfokuskan get pada namespace yang kita berika setelah query -n.

### Rolling Update & Kubernetes Manifest File

1. What is the difference between Rolling Update and Recreate deployment strategy?

   perbedaan utama strategi rolling update dan recreate deployment adalah pada recreate deployment akan terdapat downtime antara pengupdate-an aplikasi karena dengan strategi ini diperlukan mendelete dahulu aplikasi sebelumnya lalu mendeploy ulang aplikasi yang baru. Oleh karena itu akan terdapat downtime saat setelah di-delete dan selesainya deployment. Dibandingkan dengan rolling update yang mengubah aplikasi secara perlahan menjadi versi ter-upadtenya.

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt

   Akan dilaksanakan permintaan soal dengan berpanut pada blog https://dev.to/cloudskills/kubernetes-deployment-strategy-recreate-3kgn

   Akan dibuat ulang springboot-petclinic-rest yang telah di scale versi 3.0.2
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/58cee1e4-7ea6-40fe-aed4-e893e9b7523f)

   Setelah itu, akan dimanfaatkan sifat dari replicaset yang akan menggantikan pod yang terdelete dengan templatenya, maka akan diganti versi dari template nya pada settingan berikut
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/87e84bb1-42a6-4a64-9340-d475edb938b1)

   Untuk memeriksa keberhasilan perubahan lakukan query berikut yang akan menghasilkan output seperti pada gambar
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/f0da9756-5ecf-4b14-9776-9dc45f4bff86)

   Dan ketika kita delete pod kita
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/1999b365-ddb2-4603-bfad-dff57279c297)

   Dapat dilihat kalau pod-pod baru sedang dibuat untuk menggantikannya
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/0f1c0490-020f-4457-925c-5a673c23395b)

   Saat di-run akan muncul seperti demikian
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/0192b8e8-7b21-4fa5-a003-fccd2f0ab244)
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/7c2ad5f0-276e-419c-bebf-540cb27c420f)

   Sehingga bisa dinyatakan berhasil
3. Prepare different manifest files for executing Recreate deployment strategy.
   Dapat dibuat sebuah file seperti yang dilampirkan di dalam github dengan nama deployment2.yaml. Isi dari file tersebut sama seperti file hasil export pada tutorial namun terdapat perbedaan pada bagian
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/d953ba2d-10be-4f42-b360-ed3f105507c7)
   
   File tersebut bisa diimport ke dalam kubernetes seperti manifest files pada umumnya, lalu setelah itu untuk membuktikkan kalau manifest file ini memang berguna, dapat kita ganti image pada file tersebut menjadi versi yang kita inginkan dimana Ia akan mendelete pods di replica sets lama kita lalu kemudian mendeploy pods baru pada replicasets baru seperti gambar dibawah ini.
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/d8c3eb1d-b29f-40dc-aeee-36072fee1578)
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/446f9419-37fb-4352-8ef0-b1e0b1cd357f)

   Sehingga terbukti update dilakukan secara recreate strategy dan bukan rolling.

4. Keuntungan dari menggunakan manifest file jelas adalah efisiensi. Kita tidak perlu lagi mengingat prosedur dan syntax yang kita perlukan untuk melakukan update maupun deployment pertama kali. Hal ini sama saja seperti ketika kita mengimport file pada docs. Kita tidak perlu tau lagi bagaimana docs tersebut bisa menjadi seperti itu, yang penting sekarang kita sudah memiliki suatu dokumen yang siap digunakan. Hal tersebut juga berarti kita mengurangi kemungkinan terjadinya human error karena dengan manifest file, service yang terbuat sudah pasti sesuai dengan isi dari filenya dan terhindar dari kekeliruan programmer ketika mengetikkan syntaxnya satu per satu.

