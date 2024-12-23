import UIKit

class ViewController: UIViewController {
    
    var filePathTextField: UITextField!
    var searchTextField: UITextField!
    var replaceTextField: UITextField!
    var newWordTextField: UITextField!
    var resultLabel: UILabel!
    var processButton: UIButton!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        view.backgroundColor = .white
        
        filePathTextField = UITextField()
        filePathTextField.placeholder = "Caminho do arquivo"
        filePathTextField.borderStyle = .roundedRect
        filePathTextField.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(filePathTextField)
        
        searchTextField = UITextField()
        searchTextField.placeholder = "Palavra para buscar"
        searchTextField.borderStyle = .roundedRect
        searchTextField.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(searchTextField)
        
        replaceTextField = UITextField()
        replaceTextField.placeholder = "Palavra a ser substituída"
        replaceTextField.borderStyle = .roundedRect
        replaceTextField.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(replaceTextField)
        
        newWordTextField = UITextField()
        newWordTextField.placeholder = "Nova palavra"
        newWordTextField.borderStyle = .roundedRect
        newWordTextField.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(newWordTextField)
        
        resultLabel = UILabel()
        resultLabel.textAlignment = .center
        resultLabel.numberOfLines = 0
        resultLabel.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(resultLabel)
        
        processButton = UIButton(type: .system)
        processButton.setTitle("Processar", for: .normal)
        processButton.addTarget(self, action: #selector(processFile), for: .touchUpInside)
        processButton.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(processButton)
        
        NSLayoutConstraint.activate([
            filePathTextField.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 20),
            filePathTextField.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            filePathTextField.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            searchTextField.topAnchor.constraint(equalTo: filePathTextField.bottomAnchor, constant: 20),
            searchTextField.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            searchTextField.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            replaceTextField.topAnchor.constraint(equalTo: searchTextField.bottomAnchor, constant: 20),
            replaceTextField.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            replaceTextField.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            newWordTextField.topAnchor.constraint(equalTo: replaceTextField.bottomAnchor, constant: 20),
            newWordTextField.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            newWordTextField.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            resultLabel.topAnchor.constraint(equalTo: newWordTextField.bottomAnchor, constant: 20),
            resultLabel.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            resultLabel.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            
            processButton.topAnchor.constraint(equalTo: resultLabel.bottomAnchor, constant: 20),
            processButton.centerXAnchor.constraint(equalTo: view.centerXAnchor),
        ])
    }
    
    @objc func processFile() {
        guard let filePath = filePathTextField.text, !filePath.isEmpty else {
            resultLabel.text = "O caminho do arquivo não foi fornecido."
            return
        }
        
        guard FileManager.default.fileExists(atPath: filePath) else {
            resultLabel.text = "O arquivo especificado não existe."
            return
        }
        
        do {
            let content = try String(contentsOfFile: filePath, encoding: .utf8)
            
            if let searchTerm = searchTextField.text, !searchTerm.isEmpty {
                let occurrences = content.components(separatedBy: searchTerm).count - 1
                resultLabel.text = "A palavra '\(searchTerm)' aparece \(occurrences) vezes."
            }
            
            if let replaceTerm = replaceTextField.text, !replaceTerm.isEmpty,
               let newTerm = newWordTextField.text, !newTerm.isEmpty {
                let updatedContent = content.replacingOccurrences(of: replaceTerm, with: newTerm)
                try updatedContent.write(toFile: filePath, atomically: true, encoding: .utf8)
                resultLabel.text = "Substituição completa. A palavra '\(replaceTerm)' foi substituída por '\(newTerm)'."
            }
        } catch {
            resultLabel.text = "Erro ao processar o arquivo."
        }
    }
}
