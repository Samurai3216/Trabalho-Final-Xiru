Projeto final, feito a partir dos nossos conhecimentos e aprendizados durante as aulas do professor Jeferson.

📌 Sobre o Projeto

Este repositório contém um projeto em Java, focando em conceitos essenciais da linguagem, como:

Programação orientada a objetos (POO)
Manipulação de Banco de dados
Tratamento de exceções
Desenvolvimento de um CRUD completo.
O projeto visa consolidar o aprendizado e podem ser utilizados como portfólio profissional.

🛠️ Tecnologias Utilizadas

Java (JDK 17+ recomendado)
IDE: [NetBeans 8.2]
Git/GitHub para versionamento
🚀 Como Executar

Clone o repositório:

git clone https://github.com/seu-usuario/nome-do-repositorio.git 
Abra o projeto em sua IDE favorita.

Compile e execute os arquivos .java conforme necessário.

javac NomeDoArquivo.java 

java NomeDoArquivo 



📂 Estrutura do Repositório

📂 Trabalho-Final-Xiru 

├── 📁 src/main/java 

│   ├── 📁 com.exemplo.exercicios 

│   │   ├── Exercicio01.java 

│   │   ├── Exercicio02.java 

│   │ 

├── 📄 README.md 

└── 📄 .gitignore 
📖 Exemplos de Código

public class UsuarioDAO { 

private Connection con; 

 
public UsuarioDAO() throws SQLException { 
    con = ConnectionFactory.getConnection(); 
} 
 
public boolean verificarLoginSenha(String login, String password) { 
 
    String sql = "SELECT * from TB_USERS where login = ? and password = ? "; 
  PreparedStatement pst = null; 
    ResultSet rs = null; 
    Connection connection = null; 
    Boolean contemDados = null; 
 
    try { 
        connection = new ConnectionFactory().getConnection(); 
        pst = connection.prepareStatement(sql); 
        pst.setString(1, login); 
        pst.setString(2, password); 
        rs = pst.executeQuery(); 
 
        if (rs.next()) { 
            contemDados = true; 
        } else { 
            contemDados = false; 
        } 
 
    } catch (Exception e) { 
 
        e.printStackTrace(); 
        System.out.println("ERRO::OperBancoDados::verificarLoginSenha"); 
    } finally { 
        try { 
            if (pst != null) { 
                pst.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
        try { 
            if (connection != null) { 
                connection.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
 
    } 
    return contemDados; 
} 
 
public void salvarUsuarioBD(Usuario novoUsuario) { 
 
    Boolean sucesso = null; 
    String sql = "insert into TB_USERS (USER_NAME, EMAIL, LOGIN, PASSWORD, FONE_USER, CPF_USER, CEP_USER, LOGRADOURO_USER, NUMERO_USER, BAIRRO_USER, CIDADE_USER, ESTADO_USER) values (?, ?, ?, ?, ?,?, ?, ?, ?, ?,?,?)"; 
    PreparedStatement pst = null; 
    Connection connection = null; 
 
    try { 
        connection = new ConnectionFactory().getConnection(); 
        pst = connection.prepareStatement(sql); 
        pst.setString(1, novoUsuario.getNomeUsu()); 
        pst.setString(2, novoUsuario.getEmailUsu()); 
        pst.setString(3, novoUsuario.getLoginUsu()); 
        pst.setString(4, novoUsuario.getSenhaUsu()); 
        pst.setString(5, novoUsuario.getFoneUsu()); 
        pst.setString(6, novoUsuario.getCpfUsu()); 
        pst.setString(7, novoUsuario.getCepUsu()); 
        pst.setString(8, novoUsuario.getLogradouroUsu()); 
        pst.setString(9, novoUsuario.getNumeroUsu()); 
        pst.setString(10, novoUsuario.getBairroUsu()); 
        pst.setString(11, novoUsuario.getCidadeUsu()); 
        pst.setString(12, novoUsuario.getEstadoUsu()); 
        pst.executeUpdate(); 
        System.out.println("Registro inserido com sucesso no banco de dados!"); 
        sucesso = true; 
    } catch (SQLException e) { 
        e.printStackTrace(); 
        System.out.println("Login ou email existente no banco de dados!"); 
        sucesso = false; 
    } catch (Exception e) { 
        e.printStackTrace(); 
        System.out.println("ERRO::GerenciadorBancoDados::salvarUsuarioBD"); 
        sucesso = false; 
    } finally { 
        try { 
            if (pst != null) { 
                pst.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
 
        try { 
            if (connection != null) { 
                connection.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
    } 
 
} 
 
 
public ArrayList<Usuario> listarUsuarios() { 
    ArrayList<Usuario> listaUsuarios = new ArrayList<>(); 
    String sql = "SELECT id_user, user_name, email, fone_user, cep_user FROM TB_USERS";   
    PreparedStatement pst = null; 
    ResultSet rs = null; 
    Connection connection = null; 
 
    try { 
        connection = new ConnectionFactory().getConnection();   
        pst = connection.prepareStatement(sql);  
        rs = pst.executeQuery();   
 
         
        while (rs.next()) { 
            int idUsuario = rs.getInt("ID_USER");  
            String nomeP = rs.getString("USER_NAME");   
            String email = rs.getString("EMAIL");   
            String fone = rs.getString("FONE_USER");   
            String cep = rs.getString("CEP_USER");   
 
            Usuario user = new Usuario(idUsuario, fone, email, fone, cep); 
            listaUsuarios.add(user); 
             
             
        } 
 
    } catch (Exception e) { 
        e.printStackTrace();  // Exibe o erro no console, caso ocorra 
        System.out.println("Erro ao selecionar os produtos do banco de dados."); 
    } finally { 
        // Fecha os recursos (PreparedStatement, Connection) para liberar memória 
        try { 
            if (pst != null) { 
                pst.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
        try { 
            if (connection != null) { 
                connection.close(); 
            } 
        } catch (Exception e) { 
            e.printStackTrace(); 
        } 
    } 
 
    return listaUsuarios;  // Retorna a lista de produtos 
} 
  

} 

 
🏆 Autores

👤 Pedro Algayer
📧 Email: pedrogabriel308090@gmail.com
🔗 https://github.com/PedroSenac123

👤 Maurício de Campos
📧 Email: mauriciodecamposhihi@gmail.com
🔗 [LinkedIn]www.linkedin.com/in/maurício-de-campos-148005323 🔗 [GitHub] https://github.com/Samurai3216

👤 Arthur de Brito
📧 Email: arthurdebritodasilvacorinho@gmail.com
🔗 [GitHub] https://github.com/ArthurdeBrito

🎯 Objetivo do Repositório

Este repositório serve como um portfólio para demonstrar habilidades em Programação Orientada a Objetos, ajudando na busca de oportunidades de emprego na área de desenvolvimento em um futuro próximo.

⚖️ Licença

Este projeto está sob a licença MIT - veja o arquivo LICENSE para mais detalhes.
