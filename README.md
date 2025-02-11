import 'package:flutter/material.dart';

void main(){
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    home:TextFieldPage(),
  ));
}
class Staffmembers{
  String? namesurname;
  String? profession;
  int? workingperiod;

  Staffmembers({this.namesurname,this.profession,this.workingperiod});
}


class TextFieldPage extends StatefulWidget{
  @override
  State<TextFieldPage> createState()=>_TextFieldPageState();
}
class _TextFieldPageState extends State<TextFieldPage>{
  TextEditingController contentControl1=TextEditingController();
  TextEditingController contentControl2=TextEditingController();
  TextEditingController contentControl3=TextEditingController();

  List<String> names=[];
  @override
  Widget build(BuildContext context){
    return Scaffold (
      body:Center(
      child: SingleChildScrollView(
        child: Padding(padding:const EdgeInsets.all(5),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.center,
            children:[
              TextField(
                controller:contentControl1,
                decoration: InputDecoration(
                  labelText: "enter your name",
                  hintText: "name",
                  border: OutlineInputBorder(borderRadius: BorderRadius.all(Radius.circular(10)),),

                ),
              ),
            TextField(
            controller:contentControl2,
            decoration: InputDecoration(
                labelText: "enter your surname",
                hintText: "surname",
              border: OutlineInputBorder(borderRadius: BorderRadius.all(Radius.circular(10)),),
            ),
            ),
                TextField( controller:contentControl3,
              decoration: InputDecoration(
           labelText: "enter ıd",
              hintText: "ıd",
                        border: OutlineInputBorder(borderRadius: BorderRadius.all(Radius.circular(5)),),)
                ),
              Container(
                color:Colors.blue,
                width:double.infinity,
                height: MediaQuery.of(context).size.height/4,
                child:Center(
                  child:ListView.builder(
                    itemCount: names.length,
                    itemBuilder: (BuildContext context,int index){
                      return Text(
                        "${index+1}-"+ names[index],
                        style:TextStyle(fontSize:40,color:Colors.white),

                      );
                    },
                  ),
                ),
              ),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
               crossAxisAlignment: CrossAxisAlignment.center,

               children:[

                 ElevatedButton(
                   child:Text("post"),
                   onPressed: (){
                     setState(() {
                       names.add(contentControl1.text.toString()+" "+contentControl2.text.toString()+" "+contentControl3.text.toString());
                       print(contentControl1.text.toString());
                     });
                   },
                 ),
                 ElevatedButton(
                   child: Text("continue"),
                   onPressed: () {Navigator.push(context,MaterialPageRoute(builder: (context)=>TakeListPage()),);
                   },
                 ),
                   ]
                 ),
               ],
              ),
        ) ,
          ),
      ),
    );
  }
}


class TakeListPage extends StatelessWidget{
  List<Staffmembers>staffmemberlist=[
    Staffmembers(namesurname: "bünoş",profession: "parababası",workingperiod: 12),
    Staffmembers(namesurname: "yağmur",profession: "pdr",workingperiod: 16),
    Staffmembers(namesurname: "dicle",profession: "müh",workingperiod: 5),
    Staffmembers(namesurname: "taliha",profession: "mom",workingperiod: 20),
  ];
List<String>checked=[];
  String? selectedpersonel ="No";
  @override
  Widget build(BuildContext context){
    return Scaffold(
      body:Center(
      child:Column(
        children:[
          Expanded(child: ListView.builder(
            itemCount: staffmemberlist.length,
            itemBuilder: (BuildContext context,int index) {
              return ListTile(
                leading: CircleAvatar(backgroundImage: NetworkImage(""),),
                trailing: Icon(Icons.check),
                title: Text(staffmemberlist[index].namesurname!),
                subtitle: Text(
                    "profession:" + staffmemberlist[index].profession! +
                        "period:" +
                        staffmemberlist[index].workingperiod.toString()),
                onTap: () {
                  checked.add(selectedpersonel!);
                  selectedpersonel = "personel ınformation" +
                      staffmemberlist[index].namesurname!;
                  print("personel ınformation:" +
                      staffmemberlist[index].namesurname! + "short click",);
                },
              );
            },
    ),
          ),
          Text("selected personel:"+selectedpersonel!),
          ElevatedButton.icon(style:ElevatedButton.styleFrom(
    backgroundColor:Colors.blueGrey
    ),
    label:Text("close",),
    icon:Icon(Icons.save),
    onPressed: (){
            Navigator.pop(context,checked);
            checked.add("yeni eklendi");

            },
          ),
        ],
      ),
      ),
    );
  }
}


