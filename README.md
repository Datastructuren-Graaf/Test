Test
====

import java.util.*;
import java.io.*;
public class Graaf{
       private Map<String,BestemmingSet> map;
       public Graaf(){
              map = new HashMap<String,BestemmingSet>();
       }
       public int size(){
              return map.size();
       }
       public Iterator keys(){
              Iterator it = map.keySet().iterator();
              return it;
       }
       public void add(String origin, String naam, int g, int s){
                 Bestemming b = new Bestemming(naam,g,s);
                 Iterator it = keys();
                 boolean bevat = false;
                 //maakt een nieuwe MySet met de destination erin.

                 BestemmingSet des = new BestemmingSet();
                 des.add(b);

                 while(it.hasNext()){
                        String huidig = (String) it.next();
                        if(huidig.equals(origin)){
                            bevat = true;
                            des = des.union(map.get(huidig));
                            map.put(huidig,des);
                        }
                 }
                 //als map de origin NIET bevat wordt deze als nog als key toegevoegd
                 if(!(bevat)){
                       map.put(origin,des);
                 }
                 Iterator it2 = keys();
                 boolean bevat2 = false;
                 //Kijkt of de destination erin zit.
                 while(it2.hasNext()){
                      String huidig2 = (String) it2.next();
                      System.out.println(huidig2);
                      if(huidig2.equals(b.getNaam())){
                          bevat2 = true;
                      }
                 }
                 //wanneer de destination NIET in map zit wordt deze als nog toegevoegd
                 if((!bevat2)){
                    BestemmingSet leeg = new BestemmingSet();
                    map.put(b.getNaam(),leeg);
                 }
       }
       public String toString(){
              String res = "Graaf(";
              Iterator it = keys();
              while(it.hasNext()){
                  String huidig = (String) it.next();
                  res = res + "(" + huidig + "," + map.get(huidig) + ")" ;
                  if(it.hasNext()){
                       res = res + ",";
                  }
              }
              res = res + ")";
              return res;
       }
       public static void main(String[] args) {
               Graaf graaf = new Graaf();
               graaf.add("a","b",10,1);
               graaf.add("b","c",10,1);
               graaf.add("c","a",10,1);
               System.out.println(graaf);

       } 


}
