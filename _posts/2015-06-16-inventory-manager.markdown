#Home Music Inventory Manager
I created an inventory manager for my home music collection. The program creates a SQL database with three tables: music_collection, media_types, and locations. Each table can be accessed through a class: MusicCollection, MediaType and Location. The program allows a user to add, read, change and delete information from the various tables. The music collection table has 5 columns: unique id, band name, album name, media type id, and location id. The media type table has 2 columns: a unique id and type of media. The location table has 2 columns: a unique id and name of the different locations. 

##app.rb
The driver app creates a menu system that users can navigate to manipulate the various tables. 

##music.rb
The music.rb file is the file for the music_collection table for the program. 

###self.where_ find_ rows method
The self.where_ find_ rows method is a class method. It selectes all the rows from the music_collection table where field_name is a specific id number. It then pushes those objects to an Array. 

field_name - String, of the column to look in for the inputed Integer ID.
input - Integer, passed in from the user of the ID to be searching for.

```ruby
  def self.where_find_rows(field_name, input)
    results = self.find_rows(field_name, input)
    results_as_objects = []
  
    results.each do |result_hash|
    results_as_objects << MusicCollection.new(result_hash["id"], result_hash["band_name"], result_hash["album_name"], result_hash["media_type_id"], result_hash["location_id"])
    end
  
    return results_as_objects
  end
```
###self.where_ search_ rows method
The self.where_ search_ rows method is a class method that takes user input and searches the music_collection table in field_name column that matchs the search input. It then returns these as an Array of objects. 

field_name - String, the column name to search for the user inputed String.
input - String, passed in from the user using the app.rb

```ruby
  def self.where_search_rows(field_name, input)
    results = self.search_rows(field_name, input)
    results_as_objects = []
  
    results.each do |result_hash|
     results_as_objects << MusicCollection.new(result_hash["id"], result_hash["band_name"], result_hash["album_name"], result_hash["media_type_id"], result_hash["location_id"])
    end
  
    return results_as_objects
  end
```
###save method
The save method is an instance method. This method takes information performed in ruby and updates the corresponding row's information.

```ruby
  def save
    CONNECTION.execute("UPDATE music_collection SET band_name = '#{@band_name}', album_name = '#{@album_name}', media_type_id = #{@media_type_id}, location_id = #{@location_id} WHERE id = #{@id};")
    return self
  end
```

##media-type.rb, location.rb and music.rb
The media-type.rb file is the table for the different media types. The location.rb file is the table for the different locations. Both of these classes use the same 5 methods to add, find, read and delete information from their tables. Music.rb also uses these methods.

###self.all method
The self.all method is a class method that selects all of the columns from the specified table. It then creates an empty Array and pushes each object to that Array. This method returns an Array of objects. 

```ruby
  def self.all_as_objects
    results = self.all    
      results_as_objects = []
    
      results.each do |result_hash|
      results_as_objects << MusicCollection.new(result_hash["id"], result_hash["band_name"], result_hash["album_name"], result_hash["media_type_id"], result_hash["location_id"])
      end
    
      return results_as_objects
  end
```

###self.find method
The self.find method is a class method that finds an already existing row in the database and uses that to create a new object. 

id - Integer of the uniqie id of the row the method is searching for. 

```ruby
  def self.find_as_objects(id)
     @id = id
    
     result = self.find(id).first
    
     temp_band_name = result["band_name"]
     temp_album_name = result["album_name"]
     temp_media_type_id = result["media_type_id"]
     temp_location_id = result["location_id"]
    
     MusicCollection.new(id, temp_band_name, temp_album_name, temp_media_type_id, temp_location_id)
   end
```

###self.add method
The self.add method is a class method that adds a new row to the database table and then creates a new object to connect to that row.

type - a String of the type of media

```ruby
  def self.add(type)
    CONNECTION.execute("INSERT INTO media_types (type) VALUES ('#{type}');")
  
    id = CONNECTION.last_insert_row_id
  
    MediaType.new(id, type)
  end
```

###delete method
The delete method for the MediaType class and Location class check to see if the instance that is to be deleted is an empty Array. If it is empty then it will delete that instance. If the Array is not empty it will return false. The delete method for MusicCollection does not check for an empty Array.

```ruby   
 def delete_media    
    if MusicCollection.where_find_rows("media_type_id", @id) == []
      self.delete
    else
      false
    end
  end
```

###to_s method
This method will put to string whatever is inside that method. It is used in all of the classes to make the app.rb cleaner. 

