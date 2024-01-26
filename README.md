# UAS-PBO-Febricha-Avalen-07498
Project_UAS
abstract class Hewan { //class
    protected String nama; //atribut
    protected double berat;
    protected double tinggi;
    protected double panjang;

    //konstruktor
    public Hewan(String nama, double beratAwal, double tinggiAwal, double panjangAwal) {
        this.nama = nama;
        this.berat = beratAwal;
        this.tinggi = tinggiAwal;
        this.panjang = panjangAwal;
    }
//abstraction
    public abstract void tumbuh(double beratTambahan, double tinggiTambahan, double panjangTambahan);

    public abstract void displayInfo();
}

//inheritance
class Kambing extends Hewan {
    public Kambing(String nama, double beratAwal, double tinggiAwal, double panjangAwal) {
        super(nama, beratAwal, tinggiAwal, panjangAwal);
    }
//pholymorpism
    @Override
    public void tumbuh(double beratTambahan, double tinggiTambahan, double panjangTambahan) {
        this.berat += beratTambahan;
        this.tinggi += tinggiTambahan;
        this.panjang += panjangTambahan;
    }

    @Override
    public void displayInfo() {
        System.out.println("Nama: " + nama);
        System.out.println("Berat: " + berat + " kg");
        System.out.println("Tinggi: " + tinggi + " cm");
        System.out.println("Panjang: " + panjang + " cm");
    }

    public void jualAtauMati() {
        System.out.println("Kambing " + nama + " telah terjual atau mati.");
    }
}

class PemilikKambing {
    private String nama;
    private Kambing[] kambingMilik;

    public PemilikKambing(String nama, int jumlahKambing) {
        this.nama = nama;
        this.kambingMilik = new Kambing[jumlahKambing];
    }

    public void tambahKambing(String namaKambing, double beratAwal, double tinggiAwal, double panjangAwal) {
        for (int i = 0; i < kambingMilik.length; i++) {
            if (kambingMilik[i] == null) {
                kambingMilik[i] = new Kambing(namaKambing, beratAwal, tinggiAwal, panjangAwal);
                break;
            }
        }
    }
//metode
    public void perkembanganSetiapBulan(double beratTambahan, double tinggiTambahan, double panjangTambahan) {
        for (Kambing kambing : kambingMilik) {
            if (kambing != null) {
                kambing.tumbuh(beratTambahan, tinggiTambahan, panjangTambahan);
            }
        }
    }
public void displayInfoKambing() {
        for (Kambing kambing : kambingMilik) {
            if (kambing != null) {
                kambing.displayInfo();
                System.out.println("-------------------------");
            }
        }
    }

    public void jualAtauMati(String namaKambing) {
        for (int i = 0; i < kambingMilik.length; i++) {
            if (kambingMilik[i] != null && kambingMilik[i].nama.equals(namaKambing)) {
                kambingMilik[i].jualAtauMati();
                kambingMilik[i] = null;
                break;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        //object
        PemilikKambing pemilikSlamet = new PemilikKambing("Haji Slamet", 3);
        System.out.println("Data Kambing Awal Beli");
        pemilikSlamet.tambahKambing("Kambing A", 10, 80, 100);
        pemilikSlamet.tambahKambing("Kambing B", 12, 85, 110);
        pemilikSlamet.tambahKambing("Kambing C", 8, 75, 95);

        // Menampilkan informasi kambing setelah pembelian
        pemilikSlamet.displayInfoKambing();

        // Merekam perkembangan setiap bulan
        pemilikSlamet.perkembanganSetiapBulan(1, 2, 3);

        // Menampilkan informasi kambing setelah perkembangan setiap bulan
        System.out.println("Data Kambing Setelah Perkembangan Sebulan :");
        pemilikSlamet.displayInfoKambing();

        // Menandai kambing "Kambing B" sebagai terjual atau mati
        pemilikSlamet.jualAtauMati("B");

        // Menampilkan informasi kambing setelah terjual atau mati
        System.out.println("Data Kambing Setelah Terjual atau Mati :");
        pemilikSlamet.displayInfoKambing();
    }
}
