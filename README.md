# youtube
import java.util.Iterator;

import org.bson.Document;

import com.mongodb.BasicDBObject;
import com.mongodb.MongoClient;
import com.mongodb.client.FindIterable;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoCursor;
import com.mongodb.client.MongoDatabase;

public class javamongo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MongoClient mongoClient = new MongoClient("localhost", 27017);
		System.out.println("Created mongo connection successfully");
		
		// Creating datebase
		MongoDatabase db = mongoClient.getDatabase("youtube");
		System.out.println("Get database is successful");
		
		//creating collection
		
		MongoCollection<Document> collection=db.getCollection("channels");
		System.out.println("collection created");
		
		//Inserting sample records
		
		Document doc = new Document("name", "Renuka");
		doc.append("id", 100);
		doc.append("Subscribers", 1000000);
		doc.append("Genre", "programming");
		collection.insertOne(doc);
		System.out.println("Insert is completed");
		
		
		Document doc1 = new Document("name", "Naga Lakshmi");
		doc1.append("id", 102);
		doc1.append("Subscribers", 10000000);
		doc1.append("Genre", "cooking");
		collection.insertOne(doc1);
		System.out.println("Insert is completed");
		
		// Listing mongo documents
		
		FindIterable<Document> iterDoc = collection.find();
		int i = 1;
		System.out.println("Listing All mongo document");
		Iterator it = iterDoc.iterator();
		while (it.hasNext()) {
			System.out.println(it.next());
			i++;
		}
		
		//specific document retrieving in a collection
		BasicDBObject searchQuery = new BasicDBObject();
		searchQuery.put("name", "Renuka");
		System.out.println("Retrving specific mongo Documennt");
		MongoCursor<Document> cursor = collection.find(searchQuery).iterator();
		while (cursor.hasNext()) {
			System.out.println(cursor.next());
		}
		
		
		
		  
		

	}

}
