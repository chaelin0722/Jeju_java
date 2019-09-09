### LinkedList 활용한 입출력, 저장 과제



**1번 **

~~~java
import java.io.*;

class Score {
    // 학번과 이름을 저장하는 형태
    String sno;
    int score;

    Score(String data1, int data2) {
        this.sno = data1;
        this.score = data2;
    }
}

// Score 타입의 노드
class Node<T> {
    T data;
    Node<T> next;

    Node(T data, Node<T> n) {
        this.data = data;
        this.next = n;
    }
}

class LinkedList<T> {
    Node<T> head;
    Node<T> tail;

    LinkedList() {
        this.head = new Node<T>(null, null);
        this.tail = head;
    }

    public void add(T data) {
        this.tail.next = new Node<T>(data, null);
        this.tail = this.tail.next;
    }
}

public class project001 {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String l = null;
        LinkedList<Score> list = null;
        while (true) {
            System.out.println("[ M E N U ]");
            System.out.println("1. 새 자료");
            System.out.println("2. 자료 입력");
            System.out.println("3. 파일로 저장");
            System.out.println("4. 파일에서 불러오기");

            l = br.readLine();

            if (l.equals("1")) {
                list = new LinkedList<Score>();
            } else if (l.equals("2")) {
                // String l ="10101, 100"; // 학번과 성적을 linkedlist안에 저장하기
                String input = br.readLine();
                String[] input_split = input.split(",");
                Score new_data = new Score(input_split[0], Integer.parseInt(input_split[1]));
                list.add(new_data);
                System.out.println(new_data);
				/*public String toString() {
					return getClass().getName() + "@" + Integer.toHexString(hashCode());
																// 객체가 가지는 고유 번호 
				}*/
            } else if (l.equals("3")) {
                ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("a.txt"));
                Node tmp = list.head.next;
                while (tmp != null) {
                    Score s = (Score) tmp.data;
                    String line = s.sno + "," + Integer.toString(s.score);
                    out.writeUTF(line);
                    tmp = tmp.next;
                }
                out.close();
            } else if (l.equals("4")) {
                ObjectInputStream in = new ObjectInputStream(new FileInputStream("a.txt"));
                boolean keepGo = true;
                while (keepGo) {
                    try {
                        System.out.println(in.readUTF());
                    } catch (Exception e) {
                        keepGo = false;
                    }
                }
                in.close();
            } else if (l.equals("quit")) {
                break;
            }
        }
        br.close();
    }
}
~~~

**2번 **

~~~java
import java.io.*;
import java.lang.*;


// set/get 함수
// 구현체
class Node<T extends Object>{
   T data = null;
   Node<T> next = null;
   
   Node(T i, Node<T> n){
   this.data = i;
   this.next = n;
   }
}

class Score{
   private String stuNum = null;
   private String stuName = null;
   private String score = null;
   
   void setStuNum(String stuNum){
   this.stuNum = stuNum;
   }
   String getStuNum(){
   return stuNum;
   }
   
   void setStuName(String stuName){
   this.stuName = stuName;
   }
   String getStuName(){
   return stuName;
   }
   
   void setScore(String score){
   this.score = score;
   }
   String getScore(){
   return score;
   }
}

class LinkedList<U extends Object> {
      Node<U> head = null;
      Node<U> tail = null;
      
      public LinkedList(){
      this.head = new Node<U>(null, null);
      this.tail = this.head;
      }
      
      void push(U i){
         tail.next = new Node<U>(i, null);
         tail = tail.next;
      }
      
      void pop(){
         head = head.next;
      }
      
      void print() throws Exception{
         for(Node<U> n = head.next; n!=null; n= n.next) {
            // static으로 선언해서 제너러 타입을 먼저 주면 n.data 가 정의될 수있음
            DataUtil.nodePrint(n.data);
         }
      }
      
      public void save ( String fileName ) throws Exception {
      ObjectOutputStream out = new ObjectOutputStream
                              (new FileOutputStream(fileName));
      
      // out.WriteInt("데이터 갯수");
      for(Node<U> n = head.next; n!=null; n= n.next) {
            // static으로 선언해서 제너러 타입을 먼저 주면 n.data 가 정의될 수있음
            DataUtil.populate( n.data , out );
      }
      // generic 만 주어졌을 뿐이지, 접근이 불가, (타입이 정해지지 않음)
   
      out.close();
      }
      
      /*public void load(String fileName) throws IOException{
      ObjectInputStream in = new ObjectInputStream(new FileInputStream(fileName));
      Node<U> n = null;
      LinkedList<Object> ls = DataUtil.fileLoad(n.data, in);
   
      in.close();
      }*/
}

class DataUtil{
   public static void populate(Object ob, ObjectOutputStream out) throws Exception{
      if( ob instanceof Score ) {
         Score sc = (Score)ob;
         out.writeUTF(sc.getStuNum() + ", " + sc.getStuName() + ", " + sc.getScore());
      }
   }
   
   public static void nodePrint(Object ob) throws Exception{
      if( ob instanceof Score ) {
         Score sca = (Score)ob;
         System.out.println("학번 : " + sca.getStuNum() + "이름 : " + sca.getStuName() + "점수 : " + sca.getScore());
      }
   }
   
   public static Object fileLoad(Object ob, String fileName) throws Exception{
         ObjectInputStream in = new ObjectInputStream(new FileInputStream(fileName));
         String a = null;
            if( ob instanceof Score ) {
            LinkedList<Object> scoreLS = new LinkedList<Object>();
            while(true){
            try{
               a = in.readUTF();
               Score sc = new Score();
               // Score sc = (Score) ob;
               // load에서 ob는 데이터 타입을 바꿔주는 역할, 이걸 새로운 인스턴스로 생성 X
               String[] array = a.split(",");
               sc.setStuNum(array[0]);
               sc.setStuName(array[1]);
               sc.setScore(array[2]);
               
               scoreLS.push(sc);
               System.out.println(sc.getStuName());
            } catch(Exception e){
               System.out.println(e);
               break;
            }
         }
         return scoreLS;
         
         }
         
         return null;
   }
}

public class Test095{
   public static void main(String [] args) throws Exception {
      BufferedReader br = new BufferedReader( new InputStreamReader(System.in));
      
      String l = null;
      LinkedList<Score> ll = null;
      while (!("quit".equals(l))) {
      
      System.out.println("MENU");
      System.out.println("1. 새 자료");
      System.out.println("2. 자료 입력");
      System.out.println("3. 파일 저장");
      System.out.println("4. 파일에서 불러오기");
      System.out.println("5. 출력하기");

      l = br.readLine();

      if( l.equals("1")){
         ll = new LinkedList<Score>();
         System.out.println("새 자료가 생성되었습니다.");
      } else if(l.equals("2")){
            Score stu = new Score();
            System.out.print("학번을 입력해주세요");
            l = br.readLine();
            stu.setStuNum(l);
            
            System.out.print("이름을 입력해주세요");
            l = br.readLine();
            stu.setStuName(l);
            
            System.out.print("점수를 입력해주세요");
            l = br.readLine();
            stu.setScore(l);
            
            ll.push(stu);
            
         // 학번, 점수
      } else if(l.equals("3")){
         // String l = score.dat
         System.out.println("파일 이름을 입력하세요. > ");
         l = br.readLine();
         ll.save(l);
         
         // 파일 이름 받기
      } else if(l.equals("4")){
         System.out.println("파일 이름을 입력하세요. > ");
         l = br.readLine();
         ll = (LinkedList<Score>)(DataUtil.fileLoad(new Score(), l));
         ll.print();
      } else if(l.equals("5")){
         ll.print();
      }
      }
      br.close();
      
   }
   
}
~~~

