## Quick Start
Clone the repository
Install requirements
pip install -r requirements.txt

Run the script
python main.py

## Examples

Check the `example data` directory for sample files and expected outputs.

## Usage

1. Place your documents in the `example_data` folder or edit the path completely
   - Supported formats: .txt, .pdf, .docx
   - Multiple files can be processed at once

2. Run the script: python main.py


3. When prompted, you can:
   - Use the default schema for general knowledge extraction
   - Or provide a custom schema to focus on specific types of information

4. The script will:
   - Process all documents in the example_data folder
   - Create a knowledge graph in your Neo4j database
   - Display statistics about the extracted information
   - Show a visualization of the knowledge graph

## How It Works

1. **Document Processing**
   - The script reads all supported files from the example_data directory
   - Each file is processed in chunks to handle large documents
   - Text is extracted according to the file format

2. **Knowledge Extraction**
   - GPT-4 analyzes the text using the provided schema
   - Identifies entities (nodes) and their relationships
   - Extracts properties and context for both entities and relationships

3. **Graph Creation**
   - Entities become nodes in the Neo4j database
   - Relationships are created between nodes
   - Properties and context are stored with both nodes and relationships

## Visualization in Neo4j Browser

After running the script, you can visualize your knowledge graph using Neo4j Browser:

1. **Access Neo4j Browser**
   - If using Neo4j Aura:
     - Log into [Neo4j Aura Console]
     - Click on your database
     - Go on your "Query" tab, you should see the extracted nodes being uploaded there


2. **Basic Visualization Query**
   Copy and paste this query to visualize your graph:
   MATCH (n)-[r]->(m)
   RETURN DISTINCT
       LABELS(n)[0] + 
       CASE 
           WHEN n.name IS NOT NULL THEN '\n' + n.name
           ELSE ''
       END as source_label,
       
       LABELS(m)[0] + 
       CASE 
           WHEN m.name IS NOT NULL THEN '\n' + m.name
           ELSE ''
       END as target_label,
       
       TYPE(r) as relationship_label,
       
       n, r, m
   LIMIT 25;


3. **Interact with the Graph**
   - Zoom: Mouse wheel
   - Pan: Click and drag
   - Move nodes: Click and drag nodes
   - Expand nodes: Double-click
   - Select multiple: Shift + click
   - Reset view: Double-click background

4. **Additional Statistics Query**

   CALL {
       MATCH (n) RETURN COUNT(n) as node_count
   }
   CALL {
       MATCH ()-[r]->() RETURN COUNT(r) as rel_count
   }
   CALL {
       MATCH (n) 
       WITH LABELS(n) as label
       RETURN COLLECT(DISTINCT label) as node_types
   }
   CALL {
       MATCH ()-[r]->() 
       WITH TYPE(r) as type
       RETURN COLLECT(DISTINCT type) as rel_types
   }
   RETURN 
       node_count as "Total Nodes",
       rel_count as "Total Relationships",
       node_types as "Node Types",
       rel_types as "Relationship Types";


## Customization

You can customize the extraction by providing a schema when prompted. Example schema format:
  Extract relationships focusing on [YOUR_DOMAIN]:
  Nodes should include:
  -Type1: [what to extract]
  -Type2: [what to extract]
  Relationships should capture:
  -Type1 to Type2: [what to include]
  -Type2 to Type3: [what to include]
  Additional context to include:
  -[specific detail]
  -[specific detail]

## Limitations

- File size: Very large files will be processed in chunks
- API costs: Using GPT-4o incurs OpenAI API charges
- Neo4j free tier limits: Consider database size limitations
- Processing time: Large documents may take several minutes

## Troubleshooting

Common issues:
1. **API Key errors**: Ensure your OpenAI API key is valid and has available credits
2. **Neo4j connection errors**: Check your database URL format and credentials
3. **File reading errors**: Ensure files are not corrupted and in supported formats
4. **Memory issues**: Try processing smaller files or fewer files at once

## Contributing

Feel free to:
- Report issues
- Suggest improvements

