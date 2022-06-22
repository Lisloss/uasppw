## CRAWLING DATA

Data crawling adalah sebuah proses yang dilakukan untuk mengambil data besar dari sebuah halaman online yang dalam prosesnya melakukan ekstraksi data yang mengacu pada pengumpulan data berupa data dari dokumen, file, web, dan lain-lain. Data crawling merupakan proses pengambilan data yang dapat dilakukan secara cepat dan otomatis. 

## INSTALASI SCRAPY

Untuk menginstall scrapy dapat dilakukan dengan menggunakan command promt (cmd), berikut adalah code nya

```python
pip install scrapy
```

Setelah scrapy berhasil di install, selanjutnya membuat sebuah file scrapy dengan code sebagai berikut

```python
scrapy startproject nama_project
```

## MEMBUAT SPYDER

Untuk membuat sebuah file spyder yaitu masuk ke projectscrapy selanjutnya membuat sebuah file spyder yang baru dengan code sebagai berikut

```python
cd nama_project
```

Selanjutnya pada cmd yang berisi nama file yang telah dibuat dan alamat website yang akan diambil datanya

```python
scrapy genspider example example.com
```

## MEMBUAT PROGRAM SCAPPER

Setelah file yang telah dibuat sebelumnya tersimpan sesuai nama file yang telah diinginkan. Selanjutnya melakukan scraping dengan code sebagai berikut

```python
import scrapy

class scrapPTA(scrapy.Spider):
    name = 'PTA'
    allowed_domains = ['pta.trunojoyo.ac.id']
    start_urls = ['https://pta.trunojoyo.ac.id/c_search/byprod/10/'+str(x)+" " for x in range(2,20)]

    def parse(self, response):
        for link in response.css('a.gray.button::attr(href)') :
            yield response.follow(link.get(),callback=self.parse_categories)

    def parse_categories(self, response):
        products = response.css('div#content_journal ul li')
        for product in products:
            yield {
                'judul' : product.css('div a.title::text').get().strip(),
                'penulis' : product.css('div div:nth-child(2) span::text').get().strip(),
                'dosen 1' : product.css('div div:nth-child(3) span::text').get().strip(),
                'dosen 2' : product.css('div div:nth-child(4) span::text').get().strip(),
                'abstrak' : product.css('div div:nth-child(2) p::text').get().strip()
            }
```

class scrapPTA() berfungsi untuk  menspyder website

class parse berfungsi untuk melakukan follow link

## MENJALANKAN FILE SPYDER

Untuk proses ini sebelumnya masuk ke sebuah direktori lalu menjalankan spyder dengan menggunakan cmd, berikut adalah code nya

```python
scrapy runspider namafile.py
```

lalu save file tersebut dengan code sebagai berikut

```python
scrapy crawl namafile -O namafileyangdiinginkan.xlsx
```

