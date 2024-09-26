# Enkapsulasi
Enkapsulasi, yang diambil dari bahasa Inggris "encapsulation", berasal dari kata dasar "capsule" yang dapat diartikan sebagai suatu hal yang melindungi hal lain yang ada didalamnya. Konsep enkapsulasi pada bahasa pemrograman berbasis objek merupakan sebuah konsep dimana kita sebagai programmer menyembunyikan data-data sensitif dari class yang kita buat dari pengguna.

Dalam standar JavaBeans di Java, terdapat konvensi penamaan metode yang digunakan untuk mengakses dan memodifikasi properti dari suatu objek. Metode-metode tersebut dikategorikan sebagai accessor (getter), mutator (setter), dan predicate (is). Beberapa metode tersebut bisa mengontrol bagaimana suatu properti dikeluarkan dari sebuah class ataupun mengontrol perubahan dari suatu properti.

### Mengapa Enkapsulasi Penting?
Enkapsulasi pada bahasa pemrograman berorientasi objek penting karena beberapa hal.

-   Mengontrol atribut dan method dari suatu class dengan baik, tidak mudah untuk diubah dengan tidak sengaja.
-   Dapat membuat sebuah atribut atau metode kelas `read-only` atau `write-only`.
-   Membuat kode lebih modular, dapat mengubah sebuah bagian kode tanpa mengubah bagian lainnya

### Contoh Kelas Ter-enkapsulasi

```java
public class Person {
    private String full_name;
}
```

Pada contoh di atas, dapat dilihat bahwa class `Person` memiliki sebuah atribut bertipe `String` bernama `full_name` yang sifatnya `private`. Dengan access modifier private yang kita berikan, kita membuat variabel `full_name` menjadi variabel yang _encapsulated_.

Namun dengan implementasi di atas, pengguna sama sekali tidak bisa menggunakan variabel `full_name`, lalu apa guna variabel tersebut? Lihat contoh di bawah, di mana kita langsung mengakses variabel `full_name` di atas.

```java
public class Encapsulation {
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.full_name);
    }
}

class Person {
    private String full_name;
}
```

```
<< Output >>
error: full_name has private access in Person
        System.out.println(person.full_name);
                                 ^
1 error
```

Dapat dilihat bahwa Java memberikan error yang menjelaskan bahwa atribut `full_name` pada kelas `Person` memiliki akses private yang tidak bisa diakses dari luar kelas tersebut. Oleh karena itu, perlu adanya suatu method **getter**, **setter** ataupun **predicates**.

### Getter, Setter and Maybe Predicates

Getter, setter dan predicates merupakan suatu metode yang memberikan akses terbatas untuk mengakses atau memodifikasi atribut kelas yang aksesnya private. Sesuai dengan namanya, metode getter merupakan metode untuk mengakses sebuah atribut private, setter untuk memodifikasi dan predicates untuk mengecek suatu boolean.

Perhatikan sebuah contoh kelas ter-enkapsulasi di bawah ini.

```java
public class Person {
    private String name;
    private Boolean domesticated;

    public String getname() {
        return name;
    }

    public void setname(String name) {
        this.name = name;
    }

    public Boolean isDomesticated() {
        return domesticated;
    }

    public boolean isNameEmpty() {
        return this.name == null || this.name.isEmpty();
    }

}
```

Dengan konsep di atas, kita bisa mengakses method `getname()` untuk mengakses variabel `name` yang bersifat private dan `setname()` untuk mengubah nilai dari variabel `name`, lalu ada method Predicates `isDomesticated()` untuk mengakses property `domesticated`. Method `isNameEmpty()` merupakan contoh predicates, tetapi tidak sesuai standar JavaBeans.

### Contoh Penggunaan Enkapsulasi
```java
class Student {
    // Atribut atau variabel yang dienkapsulasi
    private String name;
    private String studentID;
    private double GPA;
    private Boolean graduated;

    // Getter dan Setter untuk atribut name
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // Getter dan Setter untuk atribut studentID
    public String getstudentID() {
        return studentID;
    }

    public void setstudentID(String studentID) {
        this.studentID = studentID;
    }

    // Getter dan Setter untuk atribut GPA
    public double getGPA() {
        return GPA;
    }

    public void setGPA(double GPA) {
        this.GPA = GPA;
    }

    // Predicates dan Setter untuk atribut graduated
    public boolean isGraduated() {
        return graduated;
    }

    public void setGraduated(boolean status) {
        this.graduated = status;
    }

    // Metode untuk menampilkan informasi mahasiswa
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("ID: " + studentID);
        System.out.println("GPA: " + GPA);
        if(isLulus()) {
            System.out.println("Status: Graduated");
        } else {
            System.out.println("Status: has not yet graduated");
        }
        System.out.println();
    }
}

public class Enkapsulasi {
    public static void main(String[] args) {
        Student student1 = new Student();
        student1.setName("John Doe");
        student1.setStudentID("12345678");
        student1.setGPA(3.75);
        student1.setGraduated(false);

        Student student2 = new Student();
        student2.setName("Jane Smith");
        student2.setStudentID("98765432");
        student2.setGPA(3.90);
        student2.setGraduated(false);

        System.out.println("Student 1 Information:");
        student1.displayInfo();

        System.out.println("Student 2 Information:");
        student2.displayInfo();
    }
}
```
## Facade Design Pattern

Facade Pattern adalah structural design pattern yang menyediakan interface sederhana untuk sebuah subsistem yang kompleks, sehingga lebih mudah digunakan. Facade Design membantu mengurangi dependencies dan memperlihatkan arsitektur yang lebih rapih dan terorganisir dengan cara mengenkapsulasi kompleksitas dari subsistem.

### Konsep Utama

    Subsystem: Bagian kompleks dari sistem yang sulit digunakan secara langsung.

    Facade: Sebuah kelas yang menyediakan interface sederhana ke subsystem, sehingga memudahkan klien untuk berinteraksi dengan subsystem tanpa perlu mengetahui rincian kompleksnya.

### Contoh Skenario

Mari kita pertimbangkan contoh sistem home theater, yang memiliki beberapa komponen (misalnya, pemutar DVD, proyektor, dan sound system). Alih-alih berinteraksi secara langsung dengan setiap komponen, kita dapat membuat facade yang menyederhanakan proses tersebut.

#### Contoh Subsystem

```java
// Subsystem class

class DVDPlayer {
    public void on() {
        System.out.println("Pemutar DVD menyala.");
    }

    public void play(String movie) {
        System.out.println("Memutar " + movie);
    }

    public void off() {
        System.out.println("Pemutar DVD mati.");
    }
}

class Projector {
    public void on() {
        System.out.println("Proyektor menyala.");
    }

    public void setInput(String input) {
        System.out.println("Input proyektor disetel ke " + input);
    }

    public void off() {
        System.out.println("Proyektor mati.");
    }
}

class SoundSystem {
    public void on() {
        System.out.println("Sistem Suara menyala.");
    }

    public void setVolume(int level) {
        System.out.println("Volume sistem suara disetel ke " + level);
    }

    public void off() {
        System.out.println("Sistem Suara mati.");
    }
}

```

#### Contoh Facade
```java
// Facade class

class HomeTheaterFacade {
    private DVDPlayer dvdPlayer;
    private Projector projector;
    private SoundSystem soundSystem;

    public HomeTheaterFacade() {
        dvdPlayer = new DVDPlayer();
        projector = new Projector();
        soundSystem = new SoundSystem();
    }

    public void watchMovie(String movie) {
        System.out.println("Mempersiapkan untuk menonton film...");
        dvdPlayer.on();
        projector.on();
        projector.setInput("DVD");
        soundSystem.on();
        soundSystem.setVolume(5);
        dvdPlayer.play(movie);
    }

    public void endMovie() {
        System.out.println("Mematikan teater...");
        dvdPlayer.off();
        projector.off();
        soundSystem.off();
    }
}

```

#### Penggunaan pada Client Code
```java
// Client Code
public class FacadeDemo {
    public static void main(String[] args) {
        HomeTheaterFacade homeTheater = new HomeTheaterFacade();

        homeTheater.watchMovie("Inception");
        System.out.println();
        homeTheater.endMovie();
    }
}
```