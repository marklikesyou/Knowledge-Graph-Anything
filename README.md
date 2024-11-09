## Quick Start
Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
Navigate to the project directory
cd YOUR_REPO_NAME
Install requirements
pip install -r requirements.txt
Copy example environment file
cp .env.example .env.local
Edit .env.local with your credentials
nano .env.local # or use any text editor
Run the script
python main.py

## Examples

Check the `examples/` directory for sample files and expected outputs.

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


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

4. **Visualization**
   - Creates an interactive visualization using NetworkX and Matplotlib
   - Different node types are color-coded
   - Relationships are shown as labeled arrows
   - Includes a legend for entity types

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
- Submit pull requests

