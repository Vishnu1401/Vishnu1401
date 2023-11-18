- 👋 Hi, I’m @Vishnu1401
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Vishnu1401/Vishnu1401 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
from flask import Flask, request, jsonify
from elasticsearch import Elasticsearch

app = Flask(__name__)
es = Elasticsearch()

@app.route('/ingest', methods=['POST'])
def ingest_logs():
    log_data = request.get_json()
    es.index(index='logs', body=log_data)
    return jsonify({'message': 'Logs ingested successfully'})

if __name__ == '__main__':
    app.run(port=3000)
@app.route('/search', methods=['GET'])
def search_logs():
    query_params = request.args.to_dict()
    results = es.search(index='logs', body={'query': {'match': query_params}})
    return jsonify(results)

if __name__ == '__main__':
    app.run(port=5000)  # Different port for the query interface

