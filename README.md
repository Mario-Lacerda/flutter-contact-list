# **Desafio Dio - Criando um App Flutter de Lista de Contatos**



O Flutter é um framework de desenvolvimento de aplicativos multiplataforma criado pelo Google. Ele é usado para criar aplicativos de alta qualidade para Android, iOS, web e desktop.

Neste tutorial, você aprenderá a criar um aplicativo Flutter de lista de contatos. O aplicativo terá as seguintes funcionalidades:

- A capacidade de adicionar, editar e excluir contatos.
- A capacidade de pesquisar contatos pelo nome ou número de telefone.
- A capacidade de sincronizar contatos com uma conta do Google.



## Passo 1: Criar um novo projeto Flutter

O primeiro passo é criar um novo projeto Flutter. Para fazer isso, abra o terminal e execute o seguinte comando:

```plaintext
flutter create contacts
```

Isso criará um novo diretório chamado `contacts`. Entre no diretório e abra o arquivo `pubspec.yaml`. Este arquivo é usado para gerenciar as dependências do seu projeto. Adicione as seguintes dependências ao arquivo `pubspec.yaml`:



```plaintext
dependencies:
  flutter:
    sdk: flutter
  sqflite: ^2.0.0+1
  path: ^1.8.0
  provider: ^6.0.2
```

As dependências `sqflite` e `path` são necessárias para trabalhar com banco de dados SQLite. A dependência `provider` é necessária para gerenciar o estado do aplicativo.

Agora execute o seguinte comando para instalar as dependências do seu projeto:

```plaintext
flutter pub get
```



## Passo 2: Implementar a tela inicial

A tela inicial do aplicativo será exibida quando o usuário abrir o aplicativo. Esta tela terá uma lista de contatos e um botão para adicionar um novo contato.

Para implementar a tela inicial, abra o arquivo `lib/main.dart` e adicione o seguinte código:

```plaintext
import 'package:contacts/screens/home_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Contacts',
      home: HomeScreen(),
    );
  }
}
```

O código acima cria uma instância da classe `HomeScreen` e a define como a tela inicial do aplicativo.



A classe `HomeScreen` é definida no arquivo `lib/screens/home_screen.dart`. Este arquivo contém o código para exibir a lista de contatos e o botão para adicionar um novo contato.

Abaixo está o código da classe `HomeScreen`:

```plaintext
import 'package:contacts/models/contact.dart';
import 'package:contacts/services/contact_service.dart';
import 'package:flutter/material.dart';

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  final _contactService = ContactService();
  List<Contact> _contacts = [];

  @override
  void initState() {
    super.initState();
    _getContacts();
  }

  void _getContacts() async {
    _contacts = await _contactService.getContacts();
    setState(() {});
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Contacts'),
      ),
      body: ListView.builder(
        itemCount: _contacts.length,
        itemBuilder: (context, index) {
          final contact = _contacts[index];
          return ListTile(
            title: Text(contact.name),
            subtitle: Text(contact.phoneNumber),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.add),
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(builder: (context) => AddContactScreen()),
          );
        },
      ),
    );
  }
}
```



Este código usa a classe `ContactService` para obter a lista de contatos do usuário. A lista de contatos é então exibida em uma lista. O usuário pode adicionar um novo contato tocando no botão `+` no canto inferior direito da tela.





