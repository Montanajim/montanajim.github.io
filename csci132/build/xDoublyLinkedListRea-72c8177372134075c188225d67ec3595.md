# Reading Datafile Into Linked List



## Lecture Code

```java
/*
Programmer: James Goudy
Project: Reading a csv file into a linked list
 */



import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.util.logging.Level;
import java.util.logging.Logger;

class Link {

    Link first = null;
    Link last = null;

    // data
    String id = null;
    String firstname;
    String lastname;
    String pet;
    

    // link navigation
    Link next = null;
    Link prev = null;

    // constructor
    public Link(String id, String firstname, String lastname, String pet) {
        this.id = id;
        this.firstname = firstname;
        this.lastname = lastname;
        this.pet = pet;
    }


    public void displayNode() {
        System.out.println("{"+ firstname + " " + lastname + " "
                            +pet+ " " + id +" } " );
    }
} // end of link




class Doubly {

    Link first = null;
    Link last = null;

    // constructor
    public Doubly() {

        first = null;
        last = null;
    }

    // add link at the beginning of the list
    public boolean addFirst(String id,String firstname, 
            String lastname, String pet) {
        Link newLink = new Link( id,firstname,  lastname,  pet);

        if (first == null) {
            // if list is empty
            first = newLink;
            last = newLink;
        } else {
            newLink.next = first;
            first.prev = newLink;
            first = newLink;
        }

        return true;
    }

    // add link to the end of the list
    public boolean addLast(String id,String firstname, 
            String lastname, String pet) {
        Link newLink = new Link( id,firstname,  lastname,  pet);

        if (first == null) {
            // if list is empty
            first = newLink;
            last = newLink;
        } else {
            newLink.prev = last;
            last.next = newLink;
            last = newLink;
        }

        return true;
    }

    public boolean findId(String searchID) {

        if (first == null) {

            // if list is empty
            return false;
        } else {
            Link current = first;

            while (current != null) {
                if (current.id.equals(searchID)) {
                    return true;
                }
                current = current.next;
            }

            return false;
        }
    }

    public boolean insertAfter(String searchId, String id,String firstname, 
            String lastname, String pet) {
        Link newLink = new Link( id,firstname,  lastname,  pet);

        if (first == null) {

            // list is empty - add the link
            first = newLink;
            last = newLink;

            // NOTE: there is an option not to insert
            // a link then the code above would be replaced
            // with return false
        } else {
            Link current = first;

            while (current != null) {
                if (current.id.equals(searchId)) {

                    // check if last link
                    if (current.next == null) {
                        // check if last link
                        current.next = newLink;
                        newLink.prev = current;

                        last = newLink;

                    } else {
                        newLink.next = current.next;
                        newLink.prev = current;

                        current.next.prev = newLink;
                        current.next = newLink;
                    }

                    return true;
                }
                current = current.next;

            }
        }

        return false;

    }

    public boolean insertBefore(String searchId, String id,String firstname, 
            String lastname, String pet) {

        Link newLink = new Link( id,firstname,  lastname,  pet);

        if (first == null) {

            // list is empty - add the link
            first = newLink;
            last = newLink;

            // NOTE: there is an option not to insert
            // a link then the code above would be replaced
            // with return false
        } else {
            Link current = first;

            while (current != null) {
                if (current.id.equals(searchId)) {

                    // check for first link
                    if (current.prev == null) {
                        // check if last link
                        current.prev = newLink;
                        newLink.next = current;

                        first = newLink;

                    } else {
                        newLink.next = current;
                        newLink.prev = current.prev;

                        current.prev.next = newLink;
                        current.prev = newLink;
                    }

                    return true;
                }
                current = current.next;

            }
        }

        return false;
    }

    public boolean deleteId(String searchID) {

        if (first == null) {
            return false;
        } else {
            Link current = first;

            while (current != null) {
                if (current.id.equals(searchID)) {

                    if (current.prev == null) {
                        // first node
                        current.next.prev = null;
                        first = current.next;
                        current = null;
                        return true;
                    } else if (current.next == null) {
                        // last node
                        current.prev.next = null;
                        last = current;
                        current = null;
                        return true;
                    } else {
                        // a center node
                        current.prev.next = current.next;
                        current.next.prev = current.prev;
                        current = null;

                        return true;
                    }
                }
                current = current.next;
            }

            return false;
        }
    } //end of function

    public void displayList() {
        Link current = first;

        System.out.println("");
        while (current != null) {
            current.displayNode();
            current = current.next;
        }
        System.out.println("");

    }
}

public class DS_ReadDataIntoLinkedList {

    static Doubly dl = new Doubly();

    public static void idSearch(String searchId) {

        // note that findCity returns a boolean
        // so it can be used in an "if" statement
        if (dl.findId(searchId)) {
            System.out.println("\n" + searchId + " is in list");
        } else {
            System.out.println("\n" + searchId + " not found");
        }

    }

    public static void deleteID(String searchId) {

        // note that findCity returns a boolean
        // so it can be used in an "if" statement
        if (dl.deleteId(searchId)) {
            System.out.println(searchId + " was deleted");
        } else {
            System.out.println(searchId + " was NOT deleted");
        }

    }
    
    
    public static boolean addData(String filePath)
    {
        BufferedReader br;
        FileReader fr;
        String inputLine;
        
        try {
            // create buffered reader
            br = new BufferedReader(new FileReader(filePath));
            
            // skip the header line
            br.readLine();
            
            while((inputLine = br.readLine()) != null)
            {
                String[] inputArray = inputLine.split(",");
                dl.addLast(inputArray[0],
                           inputArray[1],
                           inputArray[2],
                           inputArray[3]);
            
            }
            
            br.close();
            
        } catch (FileNotFoundException ex) {
            System.out.println(ex.getMessage());
            return false;
        }catch (Exception e)
        {
            System.out.println(e.getMessage());
            return false;
        }
        
        
        return true;
    }
    

    public static void main(String[] args) {

        String searchID = "";
        String insertCity = "";
        
        String filePath = "c:\\z\\peoplePets.csv";

        addData(filePath);

        dl.displayList();

        System.out.println("\n----- Find Examples------\n");

        searchID = "10";
        idSearch(searchID);

        searchID = "AAA";
        idSearch(searchID);

        System.out.println("\n----- Delete Examples------\n");

        searchID = "10";
        deleteID(searchID);

        searchID = "AA";
        deleteID(searchID);


        System.out.println("\n----- Insert Examples------\n");

        searchID = "140";
        dl.insertAfter(searchID, "1440","Duke","Ellington", "Phoenix");


        searchID = "145";
        dl.insertBefore(searchID, "1455","John","Coletrane", "Hydra");


        dl.displayList();

        System.out.println("\nbye");
    }
}

/* peoplePet.csv

id,firstname,lastname,pet
1,Wini,Gwinnett,Crowned hawk-eagle
2,Birgit,Tabb,Silver gull
3,Alfonso,Moyle,Ring-tailed possum
4,Ode,Buckwell,Leopard
5,Francene,Zanazzi,Wambenger
6,Willie,Hakking,Butterfly
7,Carlie,Pizey,Northern fur seal
8,Cobby,Chittock,Great white pelican
9,Ingamar,Cardenoza,Puma
10,Brady,Vowles,Red meerkat
11,Nonna,Betser,Lesser mouse lemur
12,Antonina,Dovey,Insect
13,Erastus,Crackett,Cow
14,Lucien,Cardenosa,Yellow baboon
15,Leon,Storm,Blue catfish
16,Reinaldos,Welberry,Common grenadier
17,Cherice,Coleson,Shrike
18,Elyn,Antill,Echidna
19,Dicky,Guppie,Puna ibis
20,Erasmus,Pauncefort,White-necked stork
21,Stewart,Pettifer,Starling
22,Brand,Tytcomb,Raccoon
23,Edwina,Cosens,Radiated tortoise
24,Martelle,Barkus,Cormorant
25,Blithe,Prevett,Kafue flats lechwe
26,Abbie,Ferber,Common wombat
27,Antonin,Sayes,Small-clawed otter
28,Vaughan,Barzen,Hawk-eagle
29,Elwira,Braemer,Monkey
30,Sibelle,Vennings,Javanese cormorant
31,Mavra,Bulter,Lemur
32,Darrelle,Sanford,Beisa oryx
33,Rodney,Whapples,Gull
34,Horace,Gerwood,Tropical buckeye butterfly
35,Garvin,Pestell,Bleu
36,Lauralee,Crowdace,Dama wallaby
37,Farica,Juara,Penguin
38,Bucky,Taylo,Crab
39,Carlynne,Pleasaunce,Common genet
40,Dana,Percy,White-throated kingfisher
41,Esma,McKerley,Southern ground hornbill
42,Hube,Grills,Flamingo
43,Hersch,Schneidau,Kangaroo
44,Hildy,Matfin,Gull
45,Lelia,Donaghy,American marten
46,Eric,Tydd,Bahama pintail
47,Clim,Tetsall,Spur-winged goose
48,Berke,Brotherwood,Little cormorant
49,Steve,Bride,Turtle
50,Christiane,Stoppe,Fox
51,Riley,Badgers,Swallow
52,Leonidas,Pughsley,Roseate cockatoo
53,Richard,Baudon,White-browed owl
54,Marline,Tousey,Indian mynah
55,Margarita,Breche,Phalarope
56,Gerek,Aspinwall,Great horned owl
57,Mabelle,Aronin,Grouse
58,Curtice,Provost,Indian mynah
59,Nikolaos,Cass,Desert tortoise
60,Edmund,Pogosian,Grenadier
61,Cindi,Vell,Catfish
62,Davis,Roberts,Three-banded plover
63,Clayborne,Jennrich,Roe deer
64,Malory,Iwanicki,Snowy owl
65,Toddy,Vannuchi,Arboral spiny rat
66,Terri,Dudson,Malachite kingfisher
67,Gabriel,Prine,Possum
68,Jeannine,Westwick,Gecko
69,Conney,Mattke,Stork
70,Eulalie,Wapplington,Flamingo
71,Darrick,Porcas,Rat
72,Matty,Marchment,Deer
73,Fedora,Semper,Nighthawk
74,Barnebas,Wychard,Flying fox
75,Edmund,Whitton,Squirrel
76,Oliver,Dragoe,Parrot
77,Carly,Royden,Lourie
78,Cairistiona,Brothwell,Chestnut weaver
79,Barnabas,Eastby,Lion
80,Clementina,McCoish,European stork
81,Rupert,Goosnell,Boa
82,Jerrylee,Keir,Lizard
83,Cariotta,Strettell,Little blue penguin
84,Onida,Wysome,White-rumped vulture
85,Reggis,Thursby,Cape wild cat
86,Sharleen,Yele,Gazer
87,Obadias,Rosedale,Vine snake
88,Jodie,Harmond,Boat-billed heron
89,Jonie,Goodricke,Brush-tailed phascogale
90,Carissa,Clorley,Elk
91,Jacki,Belhome,Northern elephant seal
92,Virgina,Jarrette,House sparrow
93,Hasheem,Cordeiro,Oystercatcher
94,Roseann,Hussy,Fairy penguin
95,Emmeline,Saurat,Bee-eater
96,Ashlin,Ollerhead,Grey lourie
97,Frannie,Sailes,Jungle kangaroo
98,Shelden,Imason,Woodpecker
99,Nicole,Cattle,Starling
100,Bennie,Selliman,Ant
101,Monroe,Sturzaker,Wild turkey
102,Lou,Drew-Clifton,Ferruginous hawk
103,Gerladina,Broadbere,Yellow-billed stork
104,Laney,Scartifield,Common zebra
105,Rolfe,Dressel,Cape Barren goose
106,Clarita,Zylbermann,Red-legged pademelon
107,Ev,Buckston,Kite
108,Vidovic,Lawson,Buffalo
109,Daloris,Grzesiak,Southern brown bandicoot
110,Pier,Sproson,Brocket
111,Edwina,Barlace,Giant girdled lizard
112,Elvin,Birchwood,Deer
113,Jedediah,Lazonby,Wallaby
114,Ambur,Lochead,Gila monster
115,Mirabella,Ferron,Possum
116,Dougy,Gianinotti,Openbill
117,Cher,Sivill,Dog
118,Durante,Wissby,Genet
119,Rora,Shord,Dove
120,Dame,Jennison,Red-billed toucan
121,Ira,Karolowski,Eurasian red squirrel
122,Juliet,Hobson,Greylag goose
123,Natale,Tattersdill,Starling
124,Caitlin,Leggett,Ring-necked pheasant
125,Hamnet,Danelut,South African hedgehog
126,Christye,Stores,Porcupine
127,Vince,Paolo,Kangaroo
128,Cristy,Fesby,Starling
129,Britney,Standfield,Burrowing owl
130,Kaleena,Volkers,Langur
131,Averil,Kimbell,Rhea
132,Carmelita,Gehrels,Spotted-tailed quoll
133,Cory,Sreenan,Hyrax
134,Sybille,Filippone,Dove
135,Delia,Forkan,Agama lizard
136,Sigfried,Cattlemull,Eastern dwarf mongoose
137,Rowena,James,Fox
138,Shane,Naisey,Jaguarundi
139,Janine,Ielden,Eastern fox squirrel
140,Beverlie,Biggerstaff,Fox
141,Menard,Archbould,Roe deer
142,Darline,Keating,Caribou
143,Heall,Chritchley,Beaver
144,Corenda,Bunnell,Glossy starling
145,Town,Mandal,White-winged tern
146,Pietrek,Primmer,Superb starling
147,Guillemette,Jasper,Gemsbok
148,Diane,Mewes,Civet
149,Hatty,Liddle,Grouse
150,Ange,Beardwell,Deer

 */
```



---

End Of Topic



