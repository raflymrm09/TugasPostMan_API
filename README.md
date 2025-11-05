
# TugasPostMan_API
Berikut adalah kodingan untuk Tugas Postman API :
```python
from flask import Flask, request, jsonify
app = Flask(_name_)

# Endpoint untuk cek saldo
@app.route('/api/request/cek-saldo', methods=['POST'])
def handle_request():
    try:
        # Ambil data JSON dari request body
        data = request.get_json()

        # Validasi sederhana
        if not data:
            return jsonify({
                'status': 'error',
                'message': 'Request body tidak boleh kosong'
            }), 400

        nama = data.get('nama')
        nim = data.get('nim')
        saldo = float(data.get('saldo', 0))
        nominal_transaksi = float(data.get('nominal_transaksi', 0))

        # Hitung saldo akhir
        saldo_akhir = saldo - nominal_transaksi

        # Jika saldo kurang dari nominal transaksi
        if saldo_akhir < 0:
            return jsonify({
                'status': 'fail',
                'message': f'Saldo tidak cukup untuk transaksi sebesar {nominal_transaksi}'
            }), 400

        # Jika sukses
        response_data = {
            'status': 'success',
            'message': 'Request processed successfully',
            'data': {
                'nama': nama,
                'nim': nim,
                'saldo_awal': saldo,
                'nominal_transaksi': nominal_transaksi,
                'saldo_akhir': saldo_akhir,
            },
            'news': f'Halo {nama}, data kamu sudah kami terima!'
        }

        return jsonify(response_data), 200

    except Exception as e:
        return jsonify({
            'status': 'error',
            'message': str(e)
        }), 400


if _name_ == '_main_':
    app.run(debug=True, port=5000)
```


Hasil Output: 
![Gambar WhatsApp 2025-11-05 pukul 14 44 46_07ee7c78](https://github.com/user-attachments/assets/8f54b896-970a-4645-a671-6e684ee027c7)


Bagian "nama" dan "nim" ini adalah data yang dikirim dari client (Postman), bukan yang disimpan di server.
Jadi setiap kali kamu ingin mengetes user lain (misalnya nama mahasiswa berbeda), cukup ganti nilai tersebut di body JSON pada Postman tanpa ubah kode server.
Secara keseluruhan, kode ini melakukan peningkatan kontras gambar menggunakan teknik histogram equalization.
