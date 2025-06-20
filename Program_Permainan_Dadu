#include <iostream>
#include <random>
#include <vector>
#include <algorithm>
using namespace std;

void ronde(int jumlah, int target, const vector<string>& pemain);
void tampilan_skor(int jumlah, int target, const vector<string>& pemain, const vector<int>& skor);
void tie_breaker(const vector<string>& pemain, const vector<int>& pemenang);

void play(){
    int jumlah, target, i;
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "*                      Permainan Dadu                       *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";

    do{
        cout << "Masukkan jumlah pemain : ";
        cin >> jumlah;
        if (jumlah < 1)
            cout << "Jumlah pemain tidak valid.";
    } while (jumlah < 1);

    cout << "Masukkan target skor   : ";
    cin >> target;

    vector<string> pemain(jumlah);
    cout << "\nSilakan masukkan nama pemain!\n";
    for(i = 0; i < jumlah; i++){
        cout << "Nama pemain ke-" << i + 1 << ": ";
        cin >> pemain[i];
    }
    cout << "\n            Tekan Enter untuk memulai permainan!";
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    cin.get();
    system("cls");
    ronde(jumlah, target, pemain);
}

void ronde(int jumlah, int target, const vector<string>& pemain){
    vector<int> skor(jumlah, 0);
    int i, j, nilai;

    random_device rd;
    mt19937 gen(rd());
    uniform_int_distribution<> dadu(1, 6);

    for(i = 1; i <= 3; i++){
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "*                      Permainan Dadu                       *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";
        cout << "Putaran ke-" << i << endl << endl;
        for (j = 0; j < jumlah; j++){
            nilai = dadu(gen);
            skor[j] += nilai;
            cout << "Pemain ke-" << j + 1 << ": " << pemain[j] << endl;
            cout << "Dadu Anda bernilai: " << nilai << endl;
            cout << "Skor Anda saat ini: " << skor[j] << endl << endl;
        }
        cout <<  "\n               Tekan Enter untuk melanjutkan!               ";
        cin.get();
        system("cls");
    }

   tampilan_skor(jumlah, target, pemain, skor);
}

void tampilan_skor(int jumlah, int target, const vector<string>& pemain, const vector<int>& skor) {
    vector<int> selisih(jumlah);
    vector<int> urutan(jumlah);

    for (int i = 0; i < jumlah; i++) {
        selisih[i] = abs(target - skor[i]);
    }

    iota(urutan.begin(), urutan.end(), 0);

    sort(urutan.begin(), urutan.end(), [&](int a, int b) {
        return selisih[a] < selisih[b];
    });

    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "*                      Permainan Dadu                       *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";
    cout << "Target skor = " << target << endl << endl;

    for (int i = 0; i < jumlah; i++) {
        int idx = urutan[i];
        cout << "Peringkat ke-" << i + 1 << " = " << pemain[idx] << endl;
        cout << "Skor akhir     = " << skor[idx] << endl;
        cout << "Selisih        = " << selisih[idx] << endl << endl;
    }

    int minSelisih = selisih[urutan[0]];
    vector<int> pemenang = {urutan[0]};
    for (int i = 1; i < jumlah; i++) {
        if (selisih[urutan[i]] == minSelisih) {
            pemenang.push_back(urutan[i]);
        } else {
            break; 
        }
    }

    if (pemenang.size() == 1){
        int idx = pemenang[0];
        cout << "\nPemenang permainan ini adalah " << pemain[idx] << " dengan skor " << skor[idx] << "!\n";
    } else {
        cout << "\nTerdapat lebih dari 1 pemain dengan selisih terkecil! Penentuan pemenang dilakukan melalui babak Tie-Breaker.\n";
        cout << "Tekan Enter untuk melanjutkan ke babak Tie-Breaker!";
        cin.get();
        system("cls");
        tie_breaker(pemain, pemenang);
    }

    int jawab;
    cout << "\n\nApakah Anda ingin bermain lagi?\n";
    cout << "Silakan masukkan 1 untuk bermain lagi dan karakter lainnya untuk menghentikan permainan.\n";
    cout << "Masukkan jawaban: ";
    cin >> jawab;
    if (jawab == 1){
        cin.ignore();
        system("cls");
        return;
    } else {
        system("cls");
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "*                      Permainan Dadu                       *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n\n";
        cout << "          Terima kasih sudah mencoba permainan ini!         \n\n";
        exit(0);
    }
}

void tie_breaker(const vector<string>& pemain, const vector<int>& pemenang){
    random_device rd;
    mt19937 gen(rd());
    uniform_int_distribution<> dadu(1, 6);
    
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "*                      Permainan Dadu                       *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "                       Babak Tie-Breaker                    *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";
    cout << "Pemain pada babak Tie-Breaker:\n";

    for (int idx : pemenang){
        cout << pemain[idx] << endl;
    }
    cout << "\n               Tekan Enter untuk melanjutkan!               ";
    cin.get();
    system("cls");
    
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "*                      Permainan Dadu                       *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "                       Babak Tie-Breaker                    *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";
    cout << "Pemain dengan nilai dadu terbesar akan memenangkan permainan.\n\n";
    int maxNilai = 0, idxPemenang = pemenang[0];
    for (int idx : pemenang){
        int hasil = dadu(gen);
        cout << pemain[idx] << endl;
        cout << "Nilai dadu: " << hasil << endl << endl;
        if (hasil > maxNilai){
            maxNilai = hasil;
            idxPemenang = idx;
        }
    }

    cout << "\n               Tekan Enter untuk melanjutkan!               ";
    cin.get();
    system("cls");
    
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "*                      Permainan Dadu                       *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
    cout << "                       Babak Tie-Breaker                    *\n";
    cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n";
    cout << "\nPemenang permainan ini adalah: " << pemain[idxPemenang] << "!\n";

    int jawab;
    cout << "\n\nApakah Anda ingin bermain lagi?\n";
    cout << "Silakan masukkan 1 untuk bermain lagi dan karakter lainnya untuk menghentikan permainan.\n";
    cout << "Masukkan jawaban: ";
    cin >> jawab;
    if (jawab == 1){
        cin.ignore();
        system("cls");
        return;
    } else {
        system("cls");
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "*                      Permainan Dadu                       *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n\n";
        cout << "          Terima kasih sudah mencoba permainan ini!         \n\n";
        exit(0);
    }
}

int main(){
    system("cls");
    while(true){
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "*                      Permainan Dadu                       *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n\n";
        cout << "               Tekan Enter untuk melanjutkan!               ";
        cin.get();
        system("cls");
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "*                         Tutorial                          *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n";
        cout << "* 1. Masukkan jumlah pemain terlebih dahulu.                *\n";
        cout << "*                                                           *\n";
        cout << "* 2. Masukkan target skor yang diinginkan.                  *\n";
        cout << "*                                                           *\n";
        cout << "* 3. Masukkan nama-nama pemain.                             *\n";
        cout << "*                                                           *\n";
        cout << "* 4. Setiap pemain mendapatkan kesempatan untuk melempar    *\n";
        cout << "*    dadu sebanyak 3 kali.                                  *\n";
        cout << "*                                                           *\n";
        cout << "* 5. Angka yang diperoleh akan dijumlahkan.                 *\n";
        cout << "*                                                           *\n";
        cout << "* 6. Selisih antara skor akhir pemain dengan target skor    *\n";
        cout << "*    akan dihitung.                                         *\n";
        cout << "*                                                           *\n";
        cout << "* 7. Pemenang adalah pemain dengan selisih skor akhir       *\n";
        cout << "*    terkecil dengan target skor atau nilai skor akhir      *\n";
        cout << "*    paling dekat dengan target skor.                       *\n";
        cout << "*                                                           *\n";
        cout << "* 8. Bila selisih terkecil dimiliki oleh lebih dari 1       *\n";
        cout << "*    pemain, pemain itu akan memasuki sesi tie-breaker.     *\n";
        cout << "*                                                           *\n";
        cout << "* 9. Pada sesi tie break, dadu dilempar 1 kali dan pemain   *\n";
        cout << "*    dengan angka terbesar akan memenangkan permainan.      *\n";
        cout << "* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *\n\n\n";
        cout << "               Tekan Enter untuk melanjutkan!               ";
        cin.get();
        system("cls");
        play();
    }
    return 0;
}
