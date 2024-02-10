<div align="center">
  <img src="https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Faf3291d4-361a-4ef9-a233-9be9b4312c96%2Fe32bd12f-6ffb-4c5e-a5c2-5a60b95acdce%2Fdocker-svgrepo-com.svg?table=block&id=7666d19c-f4c2-436f-a6cd-f1a1a422379a&spaceId=af3291d4-361a-4ef9-a233-9be9b4312c96&userId=9fdb15a8-c1fc-453f-a243-706bdf4c7682&cache=v2" alt="Docker Logo" width="300" height="300">
</div>

# Repo Hakkında

Bu repo, Docker öğrenme serüvenimde edindiğim bilgileri paylaşmak amacıyla oluşturuldu. Docker konusunda uzman değilim, dolayısıyla yazımda bazı hatalar olabilir. Ancak, umarım bu repo, Docker öğrenme sürecinizde size yardımcı olabilir. İçeriği okurken aklınıza takılan veya düzeltmem gereken bir şey varsa, lütfen açıkça belirtin. Keyifli okumalar.
# Docker Engine Nedir ?

Docker Engine, Docker'ın temel bileşenidir ve Docker'ın çalışmasını sağlayan çekirdek bileşenidir. Docker Engine, Docker container'larını oluşturmak, yönetmek ve çalıştırmak için gerekli olan temel hizmetleri sağlar. Docker Engine, host işletim sistemine kurulan bir yazılım olarak çalışır ve Docker container'larının çalıştığı ortamı yönetir.

Docker Engine, genellikle iki ana bileşen içerir :

1. **Docker Daemon (Docker Arka Uygulaması) :**
    - Docker Daemon, Docker Engine'in arka planda çalışan hizmetidir. Bu, Docker komutlarını alır ve ardından ilgili işlemleri gerçekleştirmek için **Docker API**'sini kullanarak container'ları oluşturur, yönetir ve izler.
    - Daemon, host işletim sistemi ile etkileşimde bulunarak container'ların oluşturulması, çalıştırılması, durdurulması ve diğer yönetim görevlerini gerçekleştirir.
2. **Docker Client (Docker İstemcisi) :**
    - Docker Client, kullanıcı ile Docker Daemon arasındaki iletişimi sağlar. Kullanıcı, Docker Client aracılığıyla Docker komutlarını çalıştırabilir ve Docker Daemon'a yönergeler verebilir.
    - Docker Client, komutları girilen bir komut satırı arayüzü (**CLI**) veya bir grafik arayüz (**Docker Desktop** gibi) aracılığıyla alabilir.

Docker Engine'in temel görevleri şunlardır :

- Docker image'larının oluşturulması ve depolanması.
- Docker container'larının oluşturulması, yönetilmesi ve çalıştırılması.
- Dockerfile'lar kullanılarak image'ların otomatik olarak oluşturulması.
- Container'ların ağ bağlantılarının yönetilmesi.
- Docker Hub gibi uzak depolama yerlerinden image'ların çekilmesi ve paylaşılması.

# Docker Image Nedir ?

Docker image, bir uygulamanın çalışması için gerekli olan tüm bağımlılıkları, ortamı ve kodu içeren bir pakettir.

Docker image'ları, birkaç temel bileşeni içerir :

1. **Base Image :** Bir Docker image'ının temelini oluşturan bu bileşen, işletim sistemi ve temel sistem araçlarını içerir. Örneğin, birçok Docker image, hafif ve yaygın olarak kullanılan Alpine Linux gibi minimalist bir Linux dağıtımını temel alabilir.
2. **Uygulama Kodu ve Bağımlılıkları :** Docker image, uygulamanın kodunu ve bağımlılıklarını içerir. Bu, uygulamanın çalıştığı dil veya çerçeve üzerindeki gereksinimleri içerir.
3. **Çalışma Zamanı Ortamı :** Docker image, uygulamanın çalıştırılabilmesi için gerekli olan çalışma zamanı ortamını (runtime environment) içerir. Bu, uygulamanın çalışması için gerekli olan her şeyi sağlar.

# Peki Docker Container’ı Nedir ?

Docker ile birlikte kullanılan "container" terimi, uygulamaların ve tüm bağımlılıklarının izole bir şekilde çalıştırılabildiği, hafif ve taşınabilir bir sanalizasyon teknolojisini ifade eder. Bir container, bir uygulamayı çalıştırmak için gerekli tüm bileşenleri içerir ve bu bileşenler izole bir ortamda bulunarak, uygulamanın bir sistemden diğerine kolayca taşınabilmesini ve tutarlı bir şekilde çalışabilmesini sağlar.

Docker Image ve Docker Container arasındaki bağlantılar şunlardır ; 

1. **Docker Container:**
    - Bir Docker container, bir Docker image'ının bir örneğidir. Yani, bir image temel alınarak çalışan bir işlem veya uygulamadır.
    - Bir konteyner, izole bir ortamda çalıştığı için kendi dosya sistemi, ağ bağlantıları ve işlem alanına sahiptir.
    - Docker container, Docker image'ının çalıştırılabilir durumudur. Birden çok container aynı image'ı temel alabilir, ancak her biri kendi izole çalışma alanına sahiptir.
2. **Docker Image:**
    - Bir Docker image, bir uygulamanın ve tüm bağımlılıklarının, çalışma zamanı ortamının ve diğer gerekli bileşenlerin bir araya getirildiği bir pakettir.
    - Docker image, bir şablondur ve bir uygulamanın nasıl çalıştırılacağını ve çevresini içerir.
    - Docker image'ları genellikle **Dockerfile** adlı metin dosyaları aracılığıyla tanımlanır ve bu dosya, bir imajın nasıl oluşturulacağını adım adım belirtir.

# Namespace ve Control Groups :

Docker, Linux işletim sisteminin temel özelliklerinden olan namespaces ve control groups (cgroups) gibi özellikleri kullanarak containerın izolasyonunu ve kaynak yönetimini sağlar. Bu özellikler, Docker Engine'in çalışma mantığının temelini oluşturur.

1. **Namespaces :**
    - Linux işletim sistemindeki namespaces, bir sürecin belirli sistem kaynaklarını izole etmesini sağlar. Bu, her bir containerın kendi izole bir ortama sahip olmasını sağlar.
    - Docker, PID (process ID), network (ağ), mount (dosya sistemi), IPC (inter-process communication), ve UTS (UNIX Time-Sharing) gibi çeşitli namespaces'leri kullanarak her konteyneri izole eder. Bu sayede, bir containerda çalışan bir sürecin diğer konteynerlerden ve host sisteminden izole olması sağlanır.
2. **Control Groups :**
    - Linux'un cgroups özelliği, sistem kaynaklarını sınırlama ve yönetme yeteneği sağlar. Her bir containerın ne kadar CPU, memory, disk I/O gibi kaynakları kullanabileceğini kontrol etmek için cgroups kullanılır.
    - Docker, her bir containerı kendi cgroup içinde izole ederek, belirli kaynakları (CPU, bellek, disk I/O, ağ bant genişliği vb.) sınırlayabilir ve yönetebilir. Bu, bir containerın diğer containerlar ve host sisteminden bağımsız olarak çalışmasını sağlar.

Docker Engine'in Linux kernel'ındaki namespaces ve control groups özelliklerini nasıl kullandığına dair genel bir akış şu şekildedir:

1. **Namespaces :**
    - Docker, her bir containerı oluştururken ve çalıştırırken, özel bir PID namespace, network namespace, mount namespace, IPC namespace ve UTS namespace oluşturur. Bu, her containerın kendi süreç ağacına, ağ bağlantılarına, dosya sistemi bağlantılarına, IPC kaynaklarına ve sistem kimlik bilgilerine sahip olduğu anlamına gelir.
2. **Control Groups (cgroups):**
    - Docker, her bir containerı oluştururken ve yönetirken, cgroups kullanarak her bir konteynerin CPU, bellek, disk I/O ve diğer kaynakları kullanımını kontrol eder. Bu, kaynakları etkin bir şekilde bölüştürmeyi ve izole etmeyi sağlar.
