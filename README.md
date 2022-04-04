- import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: BelajarAppBar(),
    );
  }
}

class BelajarAppBar extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: DefaultTabController(
        length: 3,
        child: NestedScrollView(
          headerSliverBuilder: (BuildContext context, bool innerBoxIsScrolled) {
            return <Widget>[
              SliverAppBar(
                expandedHeight: 200.0,
                floating: false,
                pinned: true,
                flexibleSpace: FlexibleSpaceBar(
                  centerTitle: true,
                  title: Text("MusikSeru",
                      style: TextStyle(
                        color: Colors.white,
                        fontWeight: FontWeight.bold,
                        fontSize: 20.0,
                      )),
                  background: Image(
                    image: AssetImage('assets/images/Mawar.jpg'),
                    fit: BoxFit.cover,
                  ),
                ),
              ),
              SliverPersistentHeader(
                pinned: true,
                delegate: _SliverAppBarDelegate(
                  TabBar(
                    labelColor: Colors.black87,
                    unselectedLabelColor: Colors.grey,
                    tabs: [
                      new Tab(icon: new Icon(Icons.audiotrack), text: "Songs"),
                      new Tab(icon: new Icon(Icons.access_alarm), text: "History"),
                      new Tab(icon: new Icon(Icons.album), text: "Albums"),
                    ],
                  ),
                ),
              ),
            ];
          },
          body: TabBarView(children: <Widget>[
            BelajarListView(),
            BelajarListView(),
            BelajarListView(),
          ]),
        ),
      ),
    );
  }
}

class BelajarListView extends StatelessWidget {
  final List bulan = [
    "In Bloom",
    "Something in the Way",
    "Lithium",
    "About A Girl",
    "Sappy",
    "Love Buzz",
    "Endless,Nameles",
    "Silver"
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: ListView.builder(
        itemBuilder: (context, index) {
          return Card(
            child: ListTile(
                title: Text(bulan[index], style: TextStyle(fontSize: 20)),
                subtitle: Text('album dari ' + bulan[index]),
                leading: CircleAvatar(
                  child: Text(bulan[index][0], // ambil karakter pertama text
                      style: TextStyle(fontSize: 20)),
                )),
          );
        },
        itemCount: bulan.length,
      ),
    );
  }
}

class _SliverAppBarDelegate extends SliverPersistentHeaderDelegate {
  _SliverAppBarDelegate(this._tabBar);

  final TabBar _tabBar;

  @override
  double get minExtent => _tabBar.preferredSize.height;
  @override
  double get maxExtent => _tabBar.preferredSize.height;

  @override
  Widget build(BuildContext context, double shrinkOffset, bool overlapsContent) {
    return new Container(
      child: _tabBar,
    );
  }

  @override
  bool shouldRebuild(_SliverAppBarDelegate oldDelegate) {
    return false;
  }
}

