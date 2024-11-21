Atividade Global Solution 2 – Energia para Um Futuro Sustentável

Nome: Ísis Castineira Nunes		RM: 93043
Nome: Rafael Heidi Satoi		RM: 94906


Sobre o aplicativo:

Nosso aplicativo foi desenvolvido para proporcionar um acompanhamento completo e em tempo real do consumo de energia em residências, indústrias ou comunidades. Por meio de gráficos interativos e opções personalizadas, ele ajuda os usuários a identificarem os maiores consumos e a adotar estratégias eficientes para economizar energia.
Nesta tela, é possível realizar o monitoramento geral.
Como podemos observar, o aplicativo apresenta gráficos que exibem o consumo total de energia em diferentes categorias, como:
•	Banho: mostra o consumo mensal relacionado ao uso do chuveiro.
•	Entretenimento: detalha o gasto energético de TVs e outros dispositivos de lazer.
•	Iluminação: analisa o consumo de lâmpadas e luminárias.
•	Dispositivos: monitora o uso de aparelhos como por exemplo: ar-condicionado, TVs e dispositivos inteligentes.
O usuário pode selecionar qualquer uma dessas categorias para, futuramente, visualizar gráficos mais detalhados sobre o consumo específico. Por exemplo, ao escolher a opção "Banho", basta clicar no botão correspondente para saber exatamente o consumo mensal de energia nessa categoria.
Já o botão xls está vinculado ao Excel. Planejamos oferecer a funcionalidade de gerar relatórios detalhados em formato Excel, que poderão ser baixados diretamente pelo app. Isso permitirá uma visualização mais organizada dos dados de consumo. No momento, estamos ajustando alguns detalhes técnicos, pois houve um problema no acesso a essa funcionalidade. Nosso objetivo é garantir que o recurso seja implementado com alta qualidade e segurança.

Para acessar a segunda tela, basta clicar no botão Dispositivos. Na segunda tela do aplicativo, você encontrará o controle inteligente dos dispositivos conectados. Nesta seção, é possível ligar ou desligar aparelhos como lâmpadas, ar-condicionado e portas inteligentes de maneira simples e intuitiva. Além disso, um gráfico de barras exibe o consumo de energia de cada dispositivo, facilitando o monitoramento. Essa funcionalidade promove não apenas maior eficiência energética, mas também oferece mais comodidade e autonomia para o usuário.


Gerenciamento de memória:
Vamos usar bibliotecas otimizadas, para os gráficos estamos usando MPAndroidChart porque é otimizada para o Android.
Estamos usando estruturas de dados que são mais adequadas para o armazenamento de dados que são somente necessários porque desse jeito conseguimos evitar um uso desnecessário de objetos.



Modelos de entidade e Automação: A partir da solução pensada, desenvolva um DER e MER para o projeto. A seguir, crie as tabelas com o auxílio de automações PL/SQL. Sendo assim, planeje rotinas com PL/SQL que seu projeto e solução possa ter. Busque inspiração nas atividades que desenvolvemos ao longo das últimas fases.

CÓDIGO SQL:

Criação de tabelas:

CREATE TABLE Usuario (
    id_usuario INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    senha VARCHAR(50),
    data_criacao DATE DEFAULT SYSDATE
);

CREATE TABLE Dispositivo (
    id_dispositivo INT PRIMARY KEY,
    id_usuario INT,
    nome VARCHAR(50),
    tipo VARCHAR(50),
    status BOOLEAN,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Consumo (
    id_consumo INT PRIMARY KEY,
    id_usuario INT,
    data TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    categoria VARCHAR(50),
    valor_consumido FLOAT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Historico_Consumo (
    id_historico INT PRIMARY KEY,
    id_usuario INT,
    data_inicio DATE,
    data_fim DATE,
    total_consumido FLOAT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);


Registro do consumo de energia:

CREATE OR REPLACE PROCEDURE registrar_consumo (
    p_id_usuario INT,
    p_categoria VARCHAR,
    p_valor_consumido FLOAT
) AS
BEGIN
    INSERT INTO Consumo (id_usuario, categoria, valor_consumido)
    VALUES (p_id_usuario, p_categoria, p_valor_consumido);
END;

Geração de relatório do consumo:

CREATE OR REPLACE FUNCTION gerar_relatorio_consumo (
    p_id_usuario INT
) RETURN SYS_REFCURSOR AS
    v_cursor SYS_REFCURSOR;
BEGIN
    OPEN v_cursor FOR
    SELECT * 
    FROM Consumo
    WHERE id_usuario = p_id_usuario
    ORDER BY data DESC;
    RETURN v_cursor;
END;


Materiais que utilizamos no desenvolvimento do nosso projeto:
Canva – é uma ferramenta online voltada para o design e comunicação visual. Utilizamos o Canva para criar os slides das apresentações em vídeo, tanto o vídeo pitch técnico quanto o vídeo pitch de vendas.

YouTube – é uma plataforma online para assistir, criar e compartilhar vídeos. Publicamos nossos vídeos, como o pitch de venda e o pitch técnico, no YouTube. 

Draw.io – é uma ferramenta online e gratuita para criação de diagramas, fluxogramas, maquetes, e muito mais. Estamos utilizando-a para desenvolver o DER e o MER do nosso projeto.

Notion – é uma plataforma que nos auxilia na organização do nosso projeto. Por meio dela, criamos uma lista de tarefas (para não esquecermos de nenhuma etapa no nosso aplicativo, na documentação, e nos vídeos), armazenamos documentos, tornando o processo do nosso projeto da Global Solution mais organizado e eficiente.

Android Studio – é uma plataforma completa para criar aplicativos Android. Como usamos o Kotlin como a linguagem de programação, o Android Studio é uma ótima opção eficiente e confiável para esse propósito.

Kotlin – é uma linguagem de programação conhecida por sua sintaxe clara e expressiva. Isso facilita a manutenção do código.

GitHub – é uma ferramenta indispensável para gerenciar o desenvolvimento do nosso aplicativo. Além de armazenar documentações, utilizamos o GitHub para que o nosso professor possa acompanhar e corrigir o nosso projeto.

Oracle SQL Developer – é um ambiente de desenvolvimento integrado (IDE) para trabalhar com SQL em banco de dados Oracle. Usamos principalmente para criar e executar os códigos SQL necessários.

Permissão de Armazenamento para o programa conseguir baixar o excel:
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

Manipulação de Excel:
import jxl.Workbook

Gráfico:
MPAndroidChart


Link do pitch de venda (até 3 minutos): https://youtu.be/j_r4hmAaTcY

Link do pitch técnico (de até 5 minutos): https://youtu.be/JrexFP1BUY4

Link do GitHub: https://github.com/RafaelSatoi/Fiap_Projects
(observação é a pasta escrito: Project_GS2)
