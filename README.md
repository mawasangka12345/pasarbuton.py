# pasarbuton.py

from flask import Flask, render_template, request, redirect
import os

app = Flask(__name__)

# Data sementara dalam daftar
barang_list = [
    {"id": 1, "nama": "Jambu Mete Lombe", "harga": "Rp 50.000", "pasar": "Pasar Lombe", "wa": "6281234567890"},
    {"id": 2, "nama": "Ikan Cakalang Segar", "harga": "Rp 35.000", "pasar": "Pasar Mawasangka", "wa": "6281234567890"}
]

@app.route('/')
def index():
    return render_template('index.html', barang=barang_list)

@app.route('/tambah', methods=['POST'])
def tambah():
    nama = request.form.get('nama')
    harga = request.form.get('harga')
    pasar = request.form.get('pasar')
    wa = request.form.get('wa')
    new_id = len(barang_list) + 1
    barang_list.append({"id": new_id, "nama": nama, "harga": harga, "pasar": pasar, "wa": wa})
    return redirect('/')

if __name__ == '__main__':
    port = int(os.environ.get("PORT", 5000))
    app.run(host='0.0.0.0', port=port)
