package com.example.search

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.Menu
import android.view.MenuItem
import androidx.appcompat.widget.SearchView
import android.widget.SearchView.OnQueryTextListener
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import java.util.*

class MainActivity : AppCompatActivity() {

    lateinit var recycleview: RecyclerView
    private lateinit var layoutManager: RecyclerView.LayoutManager
    var nameList = arrayListOf("Sasi","Sreya","Vandana","Jagadish","Aakash",
                                "Aalam","Abuna","Adair","Barbie","Bea","Byren","Busan","Casey","Cygnus","Cassie","Cordia",
                                "Dhanush","Dinesh","Darvik","Dhoni","Eminen","Edmon","Edith","Edmund",
                                "Fort","Fathima","Fariez","Farlay","Goat","Gabriel","Golmon","Gujrat",
                                "Honda","Harpix","Harry","Hut","Ian","Ileyana","Icharus","Idress","Jash",
                                "Joythish","Jasmine","Joker","Katrine","Koti","Kitchem","Kabum","London",
                                "Lyris","Lyon","Lambargini","Manish","Monish","Myth","Modern","Noris","napolean",
                                "Noish","Nap","ostrich","Onion","Octopus","Oxygen","Project","Pandya","Praveen",
                                "Preetham","Queen","Quad","Quimby","Qasim","Ramesh","Rajesh","Rohit","Riyaz",
                                "Sony","Sonu","Sazid","Salman","Tarzon","tab","Taj","Tution","Uraz","Union",
                                "Ubay","Ulin","Varun","Vohit","Vamsi","Vehivle","Wao","Walmart","Woch","Wilfeda",
                                "Xerox","Xynz","Xahir","Xyle","Yakim","Yalee","Zan","Zamir")

      lateinit var displaylist :ArrayList<String>

    private lateinit var mainAdapter: MainAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        displaylist.addAll(nameList)
        recycleview = findViewById(R.id.recycleView)
        layoutManager = LinearLayoutManager(this)
        this.mainAdapter = MainAdapter(this,displaylist)
        recycleview.adapter = mainAdapter
        recycleview.layoutManager = layoutManager
    }

    override fun onCreateOptionsMenu(menu: Menu?): Boolean {

        menuInflater.inflate(R.menu.search, menu)
        val searchItem = menu?.findItem(R.id.searchBar)
        if (searchItem != null) {
            val searchView = searchItem.actionView as SearchView
            searchView.setOnQueryTextListener(object :
                SearchView.OnQueryTextListener {
                override fun onQueryTextSubmit(query: String?): Boolean {
                    return true
                }

                override fun onQueryTextChange(newtext: String?): Boolean {
                    if (newtext!!.isNotEmpty()) {
                        displaylist.clear()
                        val search = newtext.toLowerCase(Locale.ROOT)
                        nameList.forEach {
                            if (it.toLowerCase(Locale.ROOT).contains(search)) {
                                displaylist.add(it)
                            }
                        }
                        recycleview.adapter?.notifyDataSetChanged()

                    } else {
                        displaylist.clear()
                        displaylist.addAll(nameList)
                        recycleview.adapter?.notifyDataSetChanged()
                    }
                    return true
                }

            })


        }

        return super.onCreateOptionsMenu(menu)
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        return super.onOptionsItemSelected(item)
    }
}
