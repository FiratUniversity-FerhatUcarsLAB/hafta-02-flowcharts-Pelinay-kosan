digraph OnlineAlisverisSepeti {
    rankdir=TB;
    node [shape=box, fontname="Helvetica", fontsize=10];

    Start [label="Başla", shape=oval, style=filled, fillcolor=lightgreen];
    Browse [label="Ürünleri Listele / Kategorilere Göz At"];
    ViewProduct [label="Ürün Detayını Görüntüle"];
    AddToCart [label="Ürünü Sepete Ekle"];
    ViewCart [label="Sepeti Görüntüle"];
    UpdateCart [label="Miktar Güncelle / Ürün Kaldır", shape=diamond];
    CheckEmpty [label="Sepet Boş mu?", shape=diamond];
    ApplyCoupon [label="İndirim Kodu Uygula?", shape=diamond];
    Checkout [label="Ödemeye Geç"];
    LoginChoice [label="Giriş Yapıldı mı?", shape=diamond];
    Login [label="Kullanıcı Girişi"];
    Guest [label="Misafir Olarak Devam Et"];
    Shipping [label="Teslimat Bilgilerini Gir"];
    Payment [label="Ödeme Bilgilerini Gir"];
    Confirm [label="Siparişi Onayla"];
    PaymentProcess [label="Ödeme İşleniyor..."];
    PaymentSuccess [label="Ödeme Başarılı", shape=oval, style=filled, fillc]()
