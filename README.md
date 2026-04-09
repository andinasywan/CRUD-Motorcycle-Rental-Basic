# CAPSTONE PROJECT MODULE 2 - RENTAL MOTOR
# CRUD Data Rental Motor


# Data dummy 
data_motor = [
    {
        "id_motor": "001",
        "merk": "Honda",
        "tipe": "Vario 160",
        "tahun": 2023,
        "plat_nomor": "B 1111 AAA",
        "harga_sewa_per_hari": 60000,
        "status": "Tersedia"
    },
    {
        "id_motor": "002",
        "merk": "Yamaha",
        "tipe": "NMAX",
        "tahun": 2022,
        "plat_nomor": "B 2222 BBB",
        "harga_sewa_per_hari": 80000,
        "status": "Disewa"
    },
    {
        "id_motor": "003",
        "merk": "Honda",
        "tipe": "Beat Street",
        "tahun": 2021,
        "plat_nomor": "B 3333 CCC",
        "harga_sewa_per_hari": 50000,
        "status": "Tersedia"
    }
]



# FUNGSI BANTUAN

def garis():
    print("=" * 90)


def tampilkan_judul(judul):
    garis()
    print(judul.center(90))
    garis()


def input_angka(prompt):
    while True:
        nilai = input(prompt)
        if nilai.isdigit():
            return int(nilai)
        else:
            print("Input harus berupa angka.")


def cari_index_motor(id_motor):
    for i in range(len(data_motor)):
        if data_motor[i]["id_motor"].lower() == id_motor.lower():
            return i
    return -1


def tampilkan_satu_motor(motor):
    garis()
    print(f"ID Motor             : {motor['id_motor']}")
    print(f"Merk                 : {motor['merk']}")
    print(f"Tipe                 : {motor['tipe']}")
    print(f"Tahun                : {motor['tahun']}")
    print(f"Plat Nomor           : {motor['plat_nomor']}")
    print(f"Harga Sewa per Hari  : Rp {motor['harga_sewa_per_hari']:,}")
    print(f"Status               : {motor['status']}")
    garis()


def tampilkan_semua_motor():
    if len(data_motor) == 0:
        print("Data tidak tersedia.")
        return

    garis()
    print(
        f"{'ID':<8} {'Merk':<15} {'Tipe':<20} {'Tahun':<8} {'Plat':<15} {'Harga/Hari':<15} {'Status':<10}"
    )
    garis()
    for motor in data_motor:
        print(
            f"{motor['id_motor']:<8} "
            f"{motor['merk']:<15} "
            f"{motor['tipe']:<20} "
            f"{motor['tahun']:<8} "
            f"{motor['plat_nomor']:<15} "
            f"{motor['harga_sewa_per_hari']:<15,} "
            f"{motor['status']:<10}"
        )
    garis()


def pilih_status():
    while True:
        print("Pilih status motor:")
        print("1. Tersedia")
        print("2. Disewa")
        status_pilih = input("Masukkan pilihan status (1-2): ")

        if status_pilih == "1":
            return "Tersedia"
        elif status_pilih == "2":
            return "Disewa"
        else:
            print("Pilihan status tidak valid.")



# MENU READ

def read_data():
    while True:
        tampilkan_judul("READ MENU - DATA RENTAL MOTOR")
        print("1. Tampilkan seluruh data motor")
        print("2. Cari data motor berdasarkan ID Motor")
        print("3. Kembali ke Main Menu")

        pilihan = input("Masukkan pilihan (1-3): ")

        if pilihan == "1":
            if len(data_motor) == 0:
                print("Data does not exist.")
            else:
                tampilkan_semua_motor()

        elif pilihan == "2":
            if len(data_motor) == 0:
                print("Data does not exist.")
            else:
                id_motor = input("Masukkan ID Motor yang ingin dicari: ").strip()
                index = cari_index_motor(id_motor)

                if index == -1:
                    print("Data does not exist.")
                else:
                    tampilkan_satu_motor(data_motor[index])

        elif pilihan == "3":
            break

        else:
            print("Pilihan yang Anda masukkan tidak valid.")



# MENU CREATE

def create_data():
    while True:
        tampilkan_judul("CREATE MENU - TAMBAH DATA MOTOR")
        print("1. Tambah data motor")
        print("2. Kembali ke Main Menu")

        pilihan = input("Masukkan pilihan (1-2): ")

        if pilihan == "1":
            id_motor = input("Masukkan ID Motor: ").strip()

            if cari_index_motor(id_motor) != -1:
                print("Data already exists.")
                continue

            merk = input("Masukkan merk motor: ").strip()
            tipe = input("Masukkan tipe motor: ").strip()
            tahun = input_angka("Masukkan tahun motor: ")
            plat_nomor = input("Masukkan plat nomor: ").strip().upper()
            harga_sewa_per_hari = input_angka("Masukkan harga sewa per hari: ")
            status = pilih_status()

            data_baru = {
                "id_motor": id_motor,
                "merk": merk,
                "tipe": tipe,
                "tahun": tahun,
                "plat_nomor": plat_nomor,
                "harga_sewa_per_hari": harga_sewa_per_hari,
                "status": status
            }

            print("\nData yang akan disimpan:")
            tampilkan_satu_motor(data_baru)

            simpan = input("Simpan data? (Y/N): ").strip().lower()
            if simpan == "y":
                data_motor.append(data_baru)
                print("Data successfully saved.")
            else:
                print("Data batal disimpan.")

        elif pilihan == "2":
            break

        else:
            print("Pilihan yang Anda masukkan tidak valid.")



# MENU UPDATE

def update_data():
    while True:
        tampilkan_judul("UPDATE MENU - UBAH DATA MOTOR")
        print("1. Update data motor")
        print("2. Kembali ke Main Menu")

        pilihan = input("Masukkan pilihan (1-2): ")

        if pilihan == "1":
            id_motor = input("Masukkan ID Motor yang ingin diupdate: ").strip()
            index = cari_index_motor(id_motor)

            if index == -1:
                print("The data you are looking for does not exist.")
                continue

            tampilkan_satu_motor(data_motor[index])

            lanjut = input("Lanjut update data? (Y/N): ").strip().lower()
            if lanjut != "y":
                print("Update dibatalkan.")
                continue

            print("\nKolom yang bisa diubah:")
            print("1. merk")
            print("2. tipe")
            print("3. tahun")
            print("4. plat_nomor")
            print("5. harga_sewa_per_hari")
            print("6. status")

            kolom_pilih = input("Masukkan pilihan kolom yang ingin diubah (1-6): ").strip()

            if kolom_pilih == "1":
                nilai_baru = input("Masukkan merk baru: ").strip()
                nama_kolom = "merk"

            elif kolom_pilih == "2":
                nilai_baru = input("Masukkan tipe baru: ").strip()
                nama_kolom = "tipe"

            elif kolom_pilih == "3":
                nilai_baru = input_angka("Masukkan tahun baru: ")
                nama_kolom = "tahun"

            elif kolom_pilih == "4":
                nilai_baru = input("Masukkan plat nomor baru: ").strip().upper()
                nama_kolom = "plat_nomor"

            elif kolom_pilih == "5":
                nilai_baru = input_angka("Masukkan harga sewa per hari baru: ")
                nama_kolom = "harga_sewa_per_hari"

            elif kolom_pilih == "6":
                nilai_baru = pilih_status()
                nama_kolom = "status"

            else:
                print("Kolom tidak valid.")
                continue

            print(f"\nData lama {nama_kolom}: {data_motor[index][nama_kolom]}")
            print(f"Data baru {nama_kolom}: {nilai_baru}")

            konfirmasi = input("Update data? (Y/N): ").strip().lower()
            if konfirmasi == "y":
                data_motor[index][nama_kolom] = nilai_baru
                print("Data successfully updated.")
            else:
                print("Update dibatalkan.")

        elif pilihan == "2":
            break

        else:
            print("Pilihan yang Anda masukkan tidak valid.")



# MENU DELETE

def delete_data():
    while True:
        tampilkan_judul("DELETE MENU - HAPUS DATA MOTOR")
        print("1. Hapus data motor")
        print("2. Kembali ke Main Menu")

        pilihan = input("Masukkan pilihan (1-2): ")

        if pilihan == "1":
            id_motor = input("Masukkan ID Motor yang ingin dihapus: ").strip()
            index = cari_index_motor(id_motor)

            if index == -1:
                print("The data you are looking for does not exist.")
                continue

            print("\nData yang akan dihapus:")
            tampilkan_satu_motor(data_motor[index])

            konfirmasi = input("Hapus data ini? (Y/N): ").strip().lower()
            if konfirmasi == "y":
                del data_motor[index]
                print("Data successfully deleted.")
            else:
                print("Delete dibatalkan.")

        elif pilihan == "2":
            break

        else:
            print("Pilihan yang Anda masukkan tidak valid.")



# MAIN MENU

def main_menu():
    while True:
        tampilkan_judul("PROGRAM RENTAL MOTOR")
        print("1. Read Data Motor")
        print("2. Create Data Motor")
        print("3. Update Data Motor")
        print("4. Delete Data Motor")
        print("5. Exit Program")

        pilihan = input("Masukkan pilihan menu (1-5): ")

        if pilihan == "1":
            read_data()
        elif pilihan == "2":
            create_data()
        elif pilihan == "3":
            update_data()
        elif pilihan == "4":
            delete_data()
        elif pilihan == "5":
            print("Terima kasih telah menggunakan program Rental Motor.")
            break
        else:
            print("The option you entered is not valid.")



# MENJALANKAN PROGRAM

main_menu()
