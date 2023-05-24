---
layout: post
title:  "Membuat Plugin WordPress Chat WhatsApp Rotasi CS Untuk Woocommerce"
date:   2019-03-30 19:45:31 +0530
categories: ["design", "science", "life"]
author: "Hilaludin Wahid"
---
Untuk membuat **plugin WordPress** untuk WooCommerce dengan rotasi tombol WhatsApp berdasarkan klik tombol dengan nomor WhatsApp terakhir, Anda dapat mengikuti langkah-langkah berikut:

Buat folder baru dengan nama plugin Anda di direktori wp-content/plugins.
Buat file plugin baru dengan nama plugin-name.php di folder plugin Anda.
Tambahkan header plugin Anda ke file plugin-name.php seperti ini:

{% highlight php %}
<?php
/*
Plugin Name: Nama Plugin Anda
Plugin URI: URL plugin Anda (opsional)
Description: Deskripsi singkat plugin Anda
Version: 1.0
Author: Hilaludin Wahid
Author URI: URL pengembang plugin Anda (opsional)
*/
{% endhighlight %}

4. Ini contoh kode untuk membuat whatsapp rotator di Woocommerce

{% highlight php %}
<?php
/*
Plugin Name: Simple WhatsApp Button for WooCommerce
Author: Hilaludin Wahid
Description: Menambahkan tombol WhatsApp pada halaman produk WooCommerce
Version: 1.0
*/
function rotasi_whatsapp($product_name) {
global $product;
  $product_name = get_the_title();
  $numbers = array("6287878018061", "6289605794053", "6281381261153");
  $last_number_clicked = get_option('last_number_clicked');
  if (!$last_number_clicked) {
    $last_number_clicked = 0;
  }
  $last_number_clicked++;
  if ($last_number_clicked >= count($numbers)) {
    $last_number_clicked = 0;
  }
  update_option('last_number_clicked', $last_number_clicked);
  $current_number = $numbers[$last_number_clicked];
  $url = "https://api.whatsapp.com/send?phone=".$current_number."&text=".urlencode("Hai, saya ingin membeli produk: " . $product_name);
   echo '<button id="rotasi-wa-button-click" style="background-color: green; color: white; padding: 10px 20px; border: none; border-radius: 5px;">
    <i class="fa fa-whatsapp" style="margin-right: 10px;"></i> Chat via WhatsApp
  </button>';
  
  echo '<script>
    document.getElementById("rotasi-wa-button-click").addEventListener("click", function() {
      window.location.href = "https://wa.me/' . $current_number . '";
    });
  </script>';
}



// Menambahkan action hook untuk menampilkan tombol WhatsApp
add_action('woocommerce_after_add_to_cart_form', 'rotasi_whatsapp');

{% endhighlight %}
 

 
### Catatan: 
Anda mungkin perlu menambahkan font awesome atau menggunakan icon font lainnya untuk menampilkan icon WhatsApp pada tombol. Kode di atas adalah contoh sederhana yang dapat digunakan sebagai dasar untuk pengembangan plugin Anda. Anda mungkin perlu memodifikasi kode ini sesuai dengan kebutuhan dan standar pengembangan plugin WordPress.
