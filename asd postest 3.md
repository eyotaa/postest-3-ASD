from prettytable import PrettyTable

# Node class untuk Linked List
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None

# Class untuk Linked List
class LinkedList:
    def __init__(self):
        self.head = None
        self.history = []

    def append(self, data):
        new_node = Node(data)

        # Jika Linked List kosong maka node baru menjadi head nya
        if not self.head:
            self.head = new_node
            self.history.append(f"{data} ditambahkan ke dalam Watchlist")
            return

        # Jika Linked List tidak kosong maka masukkan di akhir
        curr_node = self.head
        while curr_node.next:
            curr_node = curr_node.next
        curr_node.next = new_node
        self.history.append(f"{data} ditambahkan ke dalam Watchlist")

    def delete(self, data):
        # Jika Linked List kosong, tidak ada yang bisa dihapus
        if not self.head:
            return

        # Jika data yang ingin dihapus adalah head nya
        if self.head.data == data:
            self.head = self.head.next
            self.history.append(f"{data} dihapus dari Watchlist")
            return

        curr_node = self.head
        prev_node = None
        while curr_node and curr_node.data != data:
            prev_node = curr_node
            curr_node = curr_node.next

        # Jika tidak ditemukan simpul dengan nilai yang sesuai
        if not curr_node:
            return

        prev_node.next = curr_node.next
        self.history.append(f"{data} dihapus dari Watchlist")

    def display(self):
        x = PrettyTable()
        x.field_names = ["Watchlist Saham"]
        curr_node = self.head
        while curr_node:
            x.add_row([curr_node.data])
            curr_node = curr_node.next
        print(x)

    def display_history(self):
        x = PrettyTable()
        x.field_names = ["Histori Watchlist"]
        for item in self.history:
            x.add_row([item])
        print(x)


    def mulai(self):
        while True:
                    # Membuat table baru dengan 4 kolom: saham, harga, rekomendasi, dan keterangan
            daftar = {"saham": ['TLKM', 'BBRI', 'BBCA', 'UNVR', 'ADHI', 'WIKA', 'MNCN', 'BMRI', 'MEDC', 'PTBA'],
                    "harga": [3500, 3850, 3150, 8300, 1140, 1400, 1500, 5650, 1320, 2375, ],
                    "rekomendasi": ['beli', 'jangan beli', 'beli', 'jangan beli', 'beli', 'jangan beli',
                                    'tahan dulu', 'beli', 'jangan beli', 'tahan dulu'],
                    "keterangan": ['Harga turun dari minggu lalu', 'Harga naik terlalu cepat',
                                    'Harga stabil secara teknikal', 'Inflasi dan persaingan tinggi',
                                    'Prospek bisnis positif', 'Pengaruh pandemi masih berlangsung',
                                    'Harga belum terkonfirmasi naik maupun turun', 'Harga cukup murah',
                                    'Performa keuangan terganggu karena pandemi','Harga turun signifikan dari bulan sebelumnya']}

            tablesaham = PrettyTable()
            tablesaham.field_names = ["saham","harga","rekomendasi","keterangan"]
            tablesaham.clear_rows()
            for i in range(len(daftar["saham"])):
                tablesaham.add_row([daftar["saham"][i],daftar["harga"][i],daftar["rekomendasi"][i],daftar["keterangan"][i]])
            print(tablesaham)
            print("Program Watchlist Saham")
            print("\nDaftar Perintah:")
            print("1. Tampilkan Watchlist")
            print("2. Tambah Saham ke dalam Watchlist")
            print("3. Hapus Saham dari Watchlist")
            print("4. lihat histori")
            print("5. keluar dari program")
            print(50*"=")
            option = int(input("Perintah Anda (1/2/3/4/5): "))
            if option == 1:
                self.display()
            elif option == 2:
                a_stock = input("Masukkan nama saham yang ingin ditambahkan: ").upper()
                if a_stock in daftar['saham']:
                    self.append(a_stock)
            elif option == 3:
                h_stock = input("Masukkan nama saham yang ingin dihapus: ").upper()
                self.delete(h_stock)
            elif option == 4:
                self.display_history()
            elif option == 5:
                break
            else:
                break
m=LinkedList()
m.mulai()
