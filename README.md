# -sbasvuruformu
Form ödevi 
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: FormSayfa(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class FormSayfa extends StatefulWidget {
  @override
  State<FormSayfa> createState() => _FormSayfaState();
}

class _FormSayfaState extends State<FormSayfa> {
  final ad = TextEditingController();
  final email = TextEditingController();
  final tel = TextEditingController();
  final yas = TextEditingController();
  final deneyim = TextEditingController();
  final cv = TextEditingController();

  String? pozisyon;
  bool cvSecildi = false;

  void gonder() {
    if (ad.text.isEmpty ||
        email.text.isEmpty ||
        tel.text.isEmpty ||
        yas.text.isEmpty ||
        pozisyon == null ||
        deneyim.text.isEmpty ||
        !cvSecildi) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Text("Lütfen tüm alanları doldurun!"),
          backgroundColor: Colors.red,
        ),
      );
    } else {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Text("Başvuru başarıyla gönderildi ✔"),
          backgroundColor: Colors.green,
        ),
      );
    }
  }

  InputDecoration inputStyle(String label) {
    return InputDecoration(
      labelText: label,
      labelStyle: TextStyle(fontWeight: FontWeight.bold),
      filled: true,
      fillColor: Colors.grey[100],
      border: OutlineInputBorder(
        borderRadius: BorderRadius.circular(10),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[200],
      appBar: AppBar(
        title: Text(
          "İş Başvuru Formu",
          style: TextStyle(fontWeight: FontWeight.bold),
        ),
        backgroundColor: Colors.blue[900],
      ),
      body: SingleChildScrollView(
        child: Padding(
          padding: EdgeInsets.all(20),
          child: Column(
            children: [

              TextField(
                controller: ad,
                decoration: inputStyle("Ad Soyad"),
              ),
              SizedBox(height: 10),

              TextField(
                controller: email,
                decoration: inputStyle("E-posta"),
              ),
              SizedBox(height: 10),

              TextField(
                controller: tel,
                decoration: inputStyle("Telefon"),
              ),
              SizedBox(height: 10),

              TextField(
                controller: yas,
                decoration: inputStyle("Yaş"),
              ),
              SizedBox(height: 10),

              Container(
                padding: EdgeInsets.symmetric(horizontal: 10),
                decoration: BoxDecoration(
                  color: Colors.grey[100],
                  borderRadius: BorderRadius.circular(10),
                  border: Border.all(color: Colors.grey),
                ),
                child: DropdownButton<String>(
                  value: pozisyon,
                  hint: Text("Pozisyon seç"),
                  isExpanded: true,
                  underline: SizedBox(),
                  items: ["Yazılım", "Tasarım", "Satış", "Stajyer"]
                      .map((e) => DropdownMenuItem(
                            value: e,
                            child: Text(e),
                          ))
                      .toList(),
                  onChanged: (v) {
                    setState(() {
                      pozisyon = v;
                    });
                  },
                ),
              ),

              SizedBox(height: 10),

              TextField(
                controller: deneyim,
                maxLines: 3,
                decoration: inputStyle("Deneyim / Açıklama"),
              ),

              SizedBox(height: 10),

              // 📎 CV + DOSYA SEÇ
              Row(
                children: [
                  Expanded(
                    child: TextField(
                      controller: cv,
                      decoration: inputStyle("CV / Özgeçmiş"),
                    ),
                  ),
                  SizedBox(width: 10),

                  ElevatedButton(
                    onPressed: () {
                      setState(() {
                        cvSecildi = true;
                      });
                    },
                    child: Text("Dosya Seç"),
                  ),
                ],
              ),

              SizedBox(height: 5),

              Text(
                cvSecildi ? "CV seçildi ✔" : "CV seçilmedi",
                style: TextStyle(
                  color: cvSecildi ? Colors.green : Colors.red,
                  fontWeight: FontWeight.bold,
                ),
              ),

              SizedBox(height: 20),

              ElevatedButton(
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.blue[900],
                  padding: EdgeInsets.symmetric(vertical: 14),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(10),
                  ),
                ),
                onPressed: gonder,
                child: Text(
                  "BAŞVUR",
                  style: TextStyle(fontWeight: FontWeight.bold),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}