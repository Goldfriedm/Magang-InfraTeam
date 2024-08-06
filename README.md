# Magang-InfraTeam

## Knowledge Base
1. Apa yang anda ketahui tentang Bare Metal?
   - Bare metal adalah sebuah server fisik pada komputasi virtual yang menyediakan akses langsung ke hardware tanpa vitualisasi tambahan. Pada sistem bare metal, server fisik dikhususkan untuk satu pengguna atau satu organisasi, berbeda dengan virtualisasi seperti VPS dan lainnya
     
     Bare metal memiliki kelebihan untuk mengontrol penuh atas perangkat dan memiliki peforma yang maksimal. Hal ini didapatkan karena tidak ada overhead dari lapisan tambahan seperti sistem operasi dan hypervisor. Namun, hal ini juga menjadikan tanggung jawab lebih dalam hal manajemen perangkat keras dan keamanan.

2. Apa yang anda ketahui tentang konsep jaringan VLAN?
   - VLAN (Virtual Local Area Network) adalah metode untuk mengelompokkan perangkat dalam jaringan sehingga mereka bisa berkomunikasi seolah-olah berada dalam satu segmen LAN, meskipun sebenarnya berada di segmen LAN yang berbeda. VLAN memungkinkan beberapa jaringan IP dan subnet untuk berada dalam jaringan switch yang sama secara logis. Agar perangkat dapat berkomunikasi dalam VLAN yang sama, mereka harus memiliki alamat IP dan subnet mask yang sesuai. Switch harus dikonfigurasi dengan VLAN, dan port switch yang terdaftar di satu VLAN disebut access port.
  
3. Apa yang anda ketahui tentang IPMI/ Ip Management pada server?
   - IPMI (Intelligent Platform Management Interface) adalah sistem manajemen server yang memungkinkan admin untuk mengelola dan memonitor server secara remote tanpa mempengaruhi kinerja server. IPMI memungkinkan akses ke server bahkan saat sistem operasi tidak berfungsi, dan memungkinkan instalasi ulang sistem operasi secara remote tanpa perlu mengakses server secara fisik.

     Adapun beberapa fitur dari IPMI yaitu logging (mencatat permasalahan pada server), KVM (Keyboard Video Mouse untuk mengakses server secara remote), dan juga informasi suhu, voltage, storage dari server

4. Pernahkah anda mendesign suatu jaringan pada suatu kantor/perusahaan/campus sebutkan dan jelaskan?
   - Pernah, design jaringan pada 2 gedung kantor yang.
   - Skenario : Sebuah perusahaan prokdusi pakaian yang terdiri dari manajemen, design/kreatif, HR, dan produksi. Perusahaan mendirikan sebuah gedung kantor 2 lantai untuk tim manajemen, kreatif, dan HR, dan juga perusahaan mendirikan gedung pabrik dua lantai untuk produksi pakaian.
     
    Dengan kebutuhan jaringan :
    - Kantor lantai 2 :
        - Ruang Manajemen (7 komputer, 2 server, dan 1 printer) terhubung ke switch A dan terhubung ke router 1.
        - Ruang HR (2 komputer dan 1 printer) terhubung ke switch A dan terhubung ke router 1
    - Kantor lantai 1 :
        - Ruang Kreatif (8 komputer dan 1 printer) terhubung ke switch B dan terhubung ke router 2


    - Pabrik Produksi :
      - Ruang Produksi lantai 1 (8 komputer) terhubung ke switch C dan terhubung ke router 3
      - Ruang Pemasaran lantai 2 (5 komputer dan 1 printer) terhubung ke switch D dan terhubung ke router 4

  - Kantor dan pabrik merupakan autonomous system yang berbeda.
  - Dihubungkan host to host dengan menggunakan Cisco Packet Tracer.
  - Alamat IP perangkat yang terhubung ke jaringan menggunakan DHCP.
  - Menggunakan protokol OSPF untuk routing dinamis pada masing masing gedung.
  - Menggunakan protokol BGP(Border Gateway Protocol) untuk menghubungkan kedua gedung.



## Design Modules   

Desain Jaringan dan Alokasi IP:

Lantai 3: 

  - IT Networking (5 orang):
    - VLAN 80
    - Gateway: 192.168.80.1
    - DHCP IP Range: 192.168.80.10 - 192.168.80.15
   
  - Server Aplikasi (10 server):
    - VLAN 70
    - Gateway: 192.168.70.1
    - IP Static: 192.168.70.10 - 192.168.70.20

  - Server Database (5 server):
    - VLAN 60
    - Gateway: 192.168.60.1
    - IP Static: 192.168.60.10 - 192.168.60.15
   
Lantai 2:

  - Developer/Programmer (200 orang):
    - VLAN 50
    - Gateway: 192.168.50.1
    - DHCP IP Range: 192.168.50.10 - 192.168.50.210
   
  - Database Engineer (50 orang):
    - VLAN 40
    - Gateway: 192.168.40.1
    - DHCP IP Range: 192.168.40.10 - 192.168.40.60
   
  - QA/QC Engineer (50 orang):
    - VLAN 30
    - Gateway: 192.168.30.1
    - DHCP IP Range: 192.168.30.10 - 192.168.30.60

Lantai 1:

  - Manager (10 orang):
    - VLAN 20
    - Gateway: 192.168.20.1
    - DHCP IP Range: 192.168.20.10 - 192.168.20.20
   
  - Front Office (8 orang):
    - VLAN 10
    - Gateway: 192.168.10.1
    - DHCP IP Range: 192.168.10.10 - 192.168.10.18
   
Pengaturan Access Control List (ACL):

  - ACL VLAN 70 (Server Aplikasi):
    - Allow access dari VLAN 20 (Manager), VLAN 40 (Database Engineer), VLAN 50 (Developer/Programmer), dan VLAN 80 (IT Network).
    - Deny access dari VLAN lainnya.
   
  - ACL VLAN 60 (Server Database):
    - Allow access dari VLAN 40 (Database Engineer), VLAN 50 (Developer/Programmer), dan VLAN 80 (IT Network).
    - Deny access dari VLAN lainnya.

  - ACL VLAN 10 dan VLAN 20 (Front Office dan Manager):
    - Allow access hanya ke VLAN 20 (Server Aplikasi).
   
  - ACL VLAN 80 (IT Networking):
    - Allow access semua VLAN.
