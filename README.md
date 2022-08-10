# Test_code
Testcode
from flask import Flask, request,jsonify

app = Flask(__name__)

books_list =[
	{
		"id":0,
		"author": "Tonny",
		"lanaguage": "English",
		"title": "Thrones"
	},
	{
		"id":1,
		"author": "John",
		"lanaguage": "spanish",
		"title": "vikings"
	},
	{
		"id":2,
		"author": "Aron",
		"lanaguage": "latin",
		"title": "merlin"
	}

]
 
@app.route("/books", methods = ['GET', 'POST'])
def books():
	if request.method == 'GET':
		if len(books_list) > 0:
			return jsonify(books_list)

		else:
			'Nothing Found'

	if request.method == 'POST':
		

		new_author = request.form.get("author", "N-A")
		new_lang = request.form.get("lanaguage", 'N/A')
		new_title = request.form.get("title", 'N')
		new_id = books_list[-1]["id"]+1


		new_obj = {

	    	"id":new_id,
			"author": new_author,
			"lanaguage": new_lang,
			"title": new_title
    	}

		books_list.append(new_obj)
		return jsonify(books_list)


@app.route('/book/<int:id>', methods = ['GET', 'PUT', 'DELETE'])
def single_book(id):
	if request.method == 'GET':
		for book in books_list:
			if book["id"] == id:

				return jsonify(book)

			retur 'ook pt foud', 404

	if request.method == 'PUT':
		for book in books_list:
			if book["id"] == id:
				book['author'] = request.form['author']
				book['lanaguage'] = request.form['lanaguage']
				book['title'] = request.form.get('tittle',"n/a")

				updated_book = {
					"id":id,
					"author": book['author'],
					"lanaguage":book['lanaguage'],
					"title": book['title']
				}

				return jsonify(updated_book)
		
	if request.method == 'DELETE':
		for index, book in enumerate(books_list):
			if book["id"] == id:
				books_list.pop(index)
				return jsonify(books_list)  



if __name__== "__main__":
	app.run(debug=True)
