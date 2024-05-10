# Hello-Minikube
1. Compare the application logs before and after you exposed it as a Service.

   Ya, terdapat perbedaan karena setelah service di expose. Service dapat menerima request sehingga pada log akan tercatat request-request yang pernah terbuat, misal seperti berikut jika dilakukan refresh berkali-kali terhadap service hello-node.
   ![image](https://github.com/KenKomKom/Hello-Minikube/assets/119410845/8652396e-de55-48b6-84d3-0b44a0636afb)
2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to
`kube-system`.

  Perbedaan dari kedua syntax tersebut adalah dengan menggunakan -n, kita menyatakan kalau service yang kita mau adalah dari yang berada pada namespace tersebut. Hal ini diperlukan jika misal terdapat banyak service berbeda yang memiliki nama yang sama dan tersebar di banyak namespace. Dengan menggunakan -n, kita memfokuskan get pada namespace yang kita berika setelah query -n.


   
