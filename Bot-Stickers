import telebot
from PIL import Image

bot_token = [...]

bot = telebot.TeleBot(bot_token)

@bot.message_handler(content_types=['photo'])
def handle_photo(message):
    user_id = message.from_user.id

    file_id = message.photo[-1].file_id

    file_info = bot.get_file(file_id)
    file_path = file_info.file_path

    downloaded_file = bot.download_file(file_path)

    with open("temp.png", "wb") as new_file:
        new_file.write(downloaded_file)

    with Image.open("temp.png") as img:
        img.thumbnail((512, 512))

        img.save("temp.png", "PNG")

    new_sticker = bot.upload_sticker_file(user_id, open("temp.png", "rb"))

    bot.send_sticker(user_id, new_sticker.file_id)

    tutorial_message = "Cara Menyimpan-nya:\n\n1. Pergi ke @Stickers\n\nVIEW DI @Stickers\n\n2. Klik /Start ➡️ /newpack ( jika belum punya packnya, jika sudah punya langsung lompat ke 1. bagian bawah) ➡️ kasih nama pack (bebas)\n\n3. Kirim hasil gambar tadi atau teruskan ke @Stickers ➡️ kasih emoji (bebas) ➡️ /publish ➡️ /skip\n\n4. Kasih nama lagi (bebas, sampai berhasil tanpa ad pesan Sorry) ➡️ Klik url yg di kasih ➡️ Ketik/Klik /addsticker ➡️ Klik tombol yang muncul di keyboard / stiker yang tadi di buat\n\n5. Kalau sudah Ketik /done\n\n6. Lalu Klik url yang di kasih tadi / cara yang ke 4 tadi Selesai\n\nkalau sudah punya packnya:\n\n1. Ketik/Klik /addsticker ➡️ Klik tombol yang muncul di keyboard / stiker yang tadi di buat\n\nThank You bng dah mampir 🗿\nKalau kgk ngerti makenya tanya ama ini ae @Dika_Arya"
    bot.send_message(user_id, tutorial_message)

bot.polling()
