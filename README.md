import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyForm(),
      debugShowCheckedModeBanner: false, // Remove a etiqueta "Debug"
    );
  }
}

class MyForm extends StatefulWidget {
  @override
  _MyFormState createState() => _MyFormState();
}

class _MyFormState extends State<MyForm> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _phoneController = TextEditingController();
  final TextEditingController _emailController = TextEditingController();

  String _message = '';

  void _submitForm() {
    String name = _nameController.text;
    String email = _emailController.text;

    if (name.isEmpty || email.isEmpty) {
      setState(() {
        _message = 'Por favor, preencha todos os campos.';
      });
    } else {
      Navigator.push(
        context,
        MaterialPageRoute(
          builder: (context) => SuccessScreen(name: name),
        ),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Me contacta'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              Container(
                color: Colors.blue,
                width: double.infinity,
                padding: EdgeInsets.symmetric(vertical: 20),
                child: Text(
                  'Me conecta',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                  ),
                  textAlign: TextAlign.center,
                ),
              ),
              SizedBox(height: 10),
              TextField(
                controller: _nameController,
                decoration: InputDecoration(labelText: 'Nome Completo'),
              ),
              SizedBox(height: 10),
              TextField(
                controller: _phoneController,
                decoration: InputDecoration(labelText: 'Celular'),
                keyboardType: TextInputType.phone,
              ),
              SizedBox(height: 10),
              TextField(
                controller: _emailController,
                decoration: InputDecoration(labelText: 'E-mail'),
                keyboardType: TextInputType.emailAddress,
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () {
                  if (_nameController.text.isEmpty ||
                      _emailController.text.isEmpty ||
                      _phoneController.text.isEmpty) {
                    setState(() {
                      _message = 'Por favor, preencha todos os campos.';
                    });
                  } else {
                    _submitForm();
                  }
                },
                child: Text('Enviar'),
              ),
              SizedBox(height: 10),
              Text(
                _message,
                style: TextStyle(color: Color.fromARGB(255, 255, 0, 0)),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

class SuccessScreen extends StatelessWidget {
  final String name;

  SuccessScreen({required this.name});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Envio Concluído'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Os dados de $name foram enviados com sucesso!',
              style: TextStyle(fontSize: 18),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context); // Volta para a tela anterior
              },
              child: Text('Voltar'),
            ),
          ],
        ),
      ),
    );
  }
}

