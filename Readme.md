## Aplikasi Pemesanan Makanan

Aplikasi ini bertujuan untuk menghitung harga makanan yang di pesan seperti halnya cara kerja mesin kasir.

## Fungsionalitas
* User Dapat Menghitung Harga Barang yang dibeli dengan otomatis

* User Dapat Menambahkan Barang yang telah dibeli

## Penjelasan Kode

yang pertama membuat  Item.cs , Keranjang Belanja.cs dan Payment.cs

#### Item.cs

``` javascript

namespace Promos.Model

{

    public class Item
    {
        public string title { get; set; }
        public double price { get; set; }

        public Item(string title, double price)
        {
            this.title = title;
            this.price = price;
        }
    }
}
```

#### KeranjangBelanja.cs
Berfungsi untuk tempat barang yang sudah di tambahkan
``` javascript
class KeranjangBelanja
    {
        List<Item> itemBelanja;
        Payment payment;
        OnKeranjangBelanjaChangedListener callback;

        public KeranjangBelanja(Payment payment, OnKeranjangBelanjaChangedListener callback)
        {
            this.payment = payment;
            this.itemBelanja = new List<Item>();
            this.callback = callback;
        }
        public List<Item> getItems()
        {
            return this.itemBelanja;
        }
```

#### Payment.cs
untuk menmpilkan pembayaran barang
``` javascript

class Payment
    {
        private double deliveryFee = 0;
        private double promo = 0;
        private double balance = 0;
        private OnPaymentChangedListener paymentCallback;

        public Payment(OnPaymentChangedListener paymentCallback)
        {
            this.paymentCallback = paymentCallback;
        }

        public void setBalance(double balance)
        {
            this.balance = balance;
        }
```

Yang kedua membuat PenawaranController.cs dan MainWindoController.cs

#### PenawaranController.cs
Untuk menampilkan daftar barang 
``` csharp
 class PenawaranController
    {
        private List<Item> items;

        public PenawaranController()
        {
            items = new List<Item>();
        }

        public void addItem(Item item)
        {
            this.items.Add(item);
        }

        public List<Item> getItems()
        {
            return this.items;
        }
    }
```

#### MainWindowsController.cs
Menambahkan Item Barang ke keranjang

``` c 
 class MainWindowController
    {
        KeranjangBelanja keranjangBelanja;

        public MainWindowController(KeranjangBelanja keranjangBelanja)
        {
            this.keranjangBelanja = keranjangBelanja;
        }

        public void addItem(Item item)
        {
            this.keranjangBelanja.addItem(item);
        }
        public List<Item> getSelectedItems()
        {
            return this.keranjangBelanja.getItems();
        }
```

