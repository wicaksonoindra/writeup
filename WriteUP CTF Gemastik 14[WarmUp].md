# Writeup Gemastik 14 Pemanasan
###### 31 Juli 2002

### Forensic
##### 1. Find Me
***Temukan flag di file berikut.***
Diberikan sebuah file ASCII Text dengan nama "File", langsung cari format flag dengan perintah grep
```sh
$ cat file | grep Gemastik
Gemastik14{gunakan_grep_413ddt4}
```
Ubah Huruf kapital Gemastik14 menjadi gemastik14. Sehingga flag yang benar adalah `gemastik14{gunakan_grep_413ddt4}`

##### 2. Tzuyu
***Format flag: gemastik14{flag}***
> Hint 1: Zoom
> HInt 2: Invert

Diberikan sebuah file gambar dengan nama "TWICE_Tzuyu.png", periksa flag menggunakan aplikasi stegslove. Lalu didapatkan clue pada Red plane 3 `{canyouseeme?}`, maka flagnya adalah `gemastik14{canyouseeme?}`

##### 3. Visual is Fun

> Hint: Visualize the voice in your head

Diberikan sebuah file suara dengan nama "Visual_is_Fun.wav", cari aplikasi spectogram online. Disini kita menggunakan spectogram pada https://academo.org/articles/spectrogram/ . Setelah file dimasukkan dan dijalankan, maka grafiknya akan bertuliskan flag dengan bentuk "terbalik", yang berisi `gemastik14{visual_is_fun}`

### Steganography
##### 1. Suara dengarkanlah aku

> Catatan: format flag untuk soal ini adalah gemastik13{flag}. Mohon maaf atas ketidaknyamanannya

Terdapat file suara dengan nama file "gemastik14Sound.wav", dengan menggunakan spectogram online, kita mendapatkan grafik dengan tulisan `gemastik14{123AB}`.

##### 2. Gambar
***Temukan pesan pada gambar berikut.***
Diberikan sebuah gambar dengan nama file "TelU_Landmark_Tower.png". Dengan menggunakan stegslove, kita menemukan sebuah qr code yang berisi flag `gemastik14{hm__cobaAJA}`

##### 3. Dewi Bulan

> Seorang Dewi Bulan ditemukan sedang berjalan seorang diri di dekat sarang tupai. Ketika ditanya sang Dewi Bulan hanya mengeluarkan suara aneh yang direkam dalam file berikut. Bantu sang Dewi Bulan menemukan apa yang dia butuhkan.

Diberikan sebuah file suara dengan nama "bulan.wav", menggunakan aplikasi SSTV yang telah di install. Jalankan sstv pada terminal.
```sh
$ sstv -d bulan.wav -o result.png                    
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Robot 36
[sstv] Decoding image...   [###########################################]  99%
[sstv] Reached end of audio whilst decoding.
[sstv] Drawing image data...
[sstv] ...Done!
```
Setelah itu buka file result yang telah di dapatkan dengan sstv. Gambar tersebut memperlihatkan sebuah karakter anime dan terdapat sebuah flag di bawah gambar tersebut. Flagnya yaitu `gemastik14{4ku_butuh_kayu}`

### Reverse Engineering
##### 1. Indiana Jones
> Indiana Jones menemukan suatu peti harta karun yang terkunci. Untuk membukanya Indiana Jones memerlukan password yang dimasukkan ke dalam program verifikasi berikut. Bantu Indiana Jones menemukan kuncinya.

Terdapat file dengan nama "KodeBit.jar", extract file tersebut sehingga menghasilkan file "KodeBit.class". Lakukan decompile untuk melihat file tersebut secara online pada website http://www.javadecompilers.com/ . Lalu dihasilkan source code sebagai berikut.
```java
import java.util.ArrayList;
import java.util.Scanner;

//
// Decompiled by Procyon v0.5.36
//

public class KodeBit
{
    public static void main(final String[] array) {
        System.out.print("Enter Password: ");
        final String next = new Scanner(System.in).next();
        if (next.length() != 16) {
            System.out.println("Wrong");
            return;
        }
        final char[] array2 = { '\u0083', '\u00c3', '\u00c2', 'C', '\u0001', '\u00e1', 'B', '\u0002', 'I', '\u00e9', '\0', '#', '!', '\t', '\u00c1', '\u00c0' };
        final ArrayList<Character> list = new ArrayList<Character>();
        for (final char c : next.toCharArray()) {
            list.add((char)(((c << 5 | c >> 3) ^ 0x6F) & 0xFF));
        }
        for (int j = 0; j < 16; ++j) {
            if (!list.get(j).equals(array2[j])) {
                System.out.println("Wrong");
                return;
            }
        }
        System.out.println("Success");
    }
}
```

Disini kita dapat mengambil bagian penting flagnya saja untuk kita jalankan menjadi seperti berikut.

```java
package test;
public class Coba {
	public static void main(String[] args) {
		final char[] array2 = {'\u0083', '\u00c3', '\u00c2', 'C', '\u0001', '\u00e1', 'B', '\u0002', 'I', '\u00e9', '\0', '#', '!', '\t', '\u00c1', '\u00c0'};
		for (int i = 0; i < array2.length; i++) {
			char c = (char)(array2[i] ^ 0x6F);
			array2[i] = (char)((c >> 5 | c << 3) & 0xFF);
		}
		String s = new String(array2);
		System.out.println(s);
	}
}
```

Setelah kode tersebut dijalankan, maka akan menghasilkan flag `gemastik14{br3u}`.

### Network
##### 1. DDoS Attack
> Bantu Jhon untuk mengidentifikasi server yang terserang DDoS.
***Hint: kirim flag dengan format gemastik14{ip server}***

Terdapat sebuah file dengan nama "Attack.pcap". Setelah membaca hint yang di berikan, kita hanya perlu membuka wireshark dan melihat IP server tersebut. sehingga flagnya adalah `gemastik14{192.168.0.1}`

##### 2. Hello World
> Halo semua
Buat dapatkan flag silahkan join ke discord ini yah:
https://discord.gg/DZSRBETk

Terdapat invite link discord untuk mendapatkan file yang berisi flag. File tersebut berada di chat paling atas dengan nama file "flag.pdf". Setelah dibuka file pdf itu terlihat kosong. Namun setelah bagian kosong tersebut di block dengan cursor maupun dengan "ctrl+a" kita dapat melihat flagnya yaitu `Gemastik14{B4L4dewa}` namun flag tersebut perlu di perbaiki pada kapitalnya sehingga menjadi `gemastik14{B4L4dewa}`
