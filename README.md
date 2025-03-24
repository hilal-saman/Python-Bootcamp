# Global AI Hub Akbank Python ile Yapay Zekaya Giriş Bootcamp Sürücüsüz Metro Simülasyonu (Rota Optimizasyonu) Projesi

Bu projede bir metro ağında iki istasyon arasındaki en hızlı ve en az aktarmalı rotayı bulan bir simülasyon geliştirildi.

## Projede Kullanılan Algoritmalar

### BFS (Breadth - First Search) Algoritması

BFS algoritması en az aktarmalı rotayı hesaplamak için kullanılır. Bu algoritma genişleme esaslıdır ve her seferinde bir sonraki seviye istasyonlarını keşfeder. Hedef istasyonuna vardığında en kısa rotayı döndürür.

#### BFS Algoritmasının Çalışma Adımları

1. Başlangıç veya hedef istasyon yoksa None döndür.
2. BFS için bir kuyruk (deque) oluştur ve başlangıç istasyonunu içine ekle.
3. Ziyaret edilen istasyonları takip etmek için bir set oluştur.
4. BFS döngüsünü başlat:
    - Kuyruktan bir istasyon al.
    - Hedef istasyona ulaşıldıysa, izlenen rotayı döndür.
    - Komşu istasyonları kontrol et:
        - Daha önce ziyaret edilmediyse:
            - Ziyaret edilenler setine ekle.
            - Yeni rotayı oluştur.
            - Kuyruğa ekle.
5. Hiçbir rota bulunamazsa None döndür.
### A* Algoritması

A* algoritması en hızlı rotayı bulmak için kullanılır. Bu algoritma her adımda en düşük maliyete sahip rotayı genişletir.A* algoritması hem gidilen mesafeyi hem de hedefe olan mesafeyi dikkate alarak en kısa yolu bulur.

#### A* Algoritmasının Çalışma Adımları

1. Başlangıç veya hedef istasyon yoksa None döndür.
2. Öncelikli bir kuyruk (heapq) oluştur ve başlangıç istasyonunu ekle.
3. Ziyaret edilen istasyonları takip etmek için bir set oluştur.
4. A* döngüsünü başlat:
    - Kuyruktan en düşük maliyetli istasyonu al.
    - Hedefe ulaşıldıysa, izlenen rotayı ve toplam süreyi döndür.
    - Komşu istasyonları kontrol et:
        - Daha önce ziyaret edilmediyse:
            - Yeni toplam süreyi hesapla.
            - Ziyaret edilenler setine ekle.
            - Yeni rotayı oluştur.
            - Öncelik kuyruğuna ekle.

5. Hiçbir rota bulunamazsa None döndür.

## Kullanılan Teknolojiler Ve Kütüphaneler

#### 1. Python

Proje Python programlama dili kullanılarak geliştirilmiştir.

#### 2. Collections Modülü

Python'da collections modülü daha güçlü veri yapıları sunar. Bu projede iki ana yapıyı kullanıyoruz:

- deque: Çift taraflı kuyruk yapısıdır. Bu yapı sayesinde BFS algoritmasında kuyruk kullanarak istasyonları seviyeli bir şekilde genişletebiliriz. deque, listelere göre daha hızlı ekleme ve çıkarma işlemleri yapar.

- defaultdict: Varsayılan değer atanmış sözlüklerdir. Bu yapı metro ağı üzerindeki hatları ve istasyonları modellemeyi daha kolay hale getirir.

#### 3. Heapq Modülü

heapq modülü, Python'da öncelik kuyruğu (priority queue) oluşturmak için kullanılır. Bu projede A* algoritmasında en kısa süreli rotayı seçmek için heap yapısını kullanıyoruz. heapq, her zaman en düşük maliyeti (süreyi) öncelikli hale getirir ve algoritmanın verimli çalışmasını sağlar.

#### 4. Typing Modülü

typing modülü, Python'da değişkenlerin ve fonksiyonların tiplerini belirtmemize olanak tanır. Bu projede istasyonları ve metro ağını daha kolay yönetmek için List, Dict, Tuple ve Optional gibi tür ipuçlarını kullanıyoruz. Bu da kodun okunabilirliğini ve anlaşılabilirliğini artırır.

## Örnek Test Senaryoları

    # Senaryo 1: AŞTİ'den OSB'ye
    print("\n1. AŞTİ'den OSB'ye:")
    rota = metro.en_az_aktarma_bul("M1", "K4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("M1", "K4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
    
    # Senaryo 2: Batıkent'ten Keçiören'e
    print("\n2. Batıkent'ten Keçiören'e:")
    rota = metro.en_az_aktarma_bul("T1", "T4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("T1", "T4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))

### Test Sonuçları

=== Test Senaryoları ===

1.AŞTİ'den OSB'ye:
En az aktarmalı rota: AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB
En hızlı rota (25 dakika): AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB

2.Batıkent'ten Keçiören'e:
En az aktarmalı rota: Batıkent -> Demetevler -> Gar -> Keçiören
En hızlı rota (21 dakika): Batıkent -> Demetevler -> Gar -> Keçiören

## Projeyi Geliştrime Fikirleri

- Diğer toplu taşıma araçları eklenebilir.
- Toplu taşıma araçlarının gerçek zamanları (istediğimiz noktada saat kaçta olacakları) eklenebilir.
