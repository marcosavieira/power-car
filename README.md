
openapi: 3.0.0
info:
  title: API VEICULAR
  description: Api para ERP de manutenção veicular
  version: 1.0.0
paths:
  /pessoas:
    get:
      tags:
        - Pessoas
      summary: Lista todas as pessoas
      operationId: 3dc616a61eacfedcb301f11adb7fcaa1
      responses:
        '200':
          description: Lista de todas as pessoas
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Pessoa'
        '500':
          description: Erro ao obter a lista de pessoas
    post:
      tags:
        - Pessoas
      summary: Cria uma nova pessoa
      operationId: 0269fc659827ad5bbdcde3393b59309b
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Pessoa'
      responses:
        '201':
          description: Pessoa criada com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Pessoa'
        '400':
          description: Erro de validação
        '500':
          description: Erro ao criar uma nova pessoa
  /pessoas/{id}:
    get:
      tags:
        - Pessoas
      summary: Lista uma pessoa específica
      operationId: ed509b9d131a64e29eb74abcffb6f579
      parameters:
        - name: id
          in: path
          description: ID da pessoa
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Pessoa encontrada
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Pessoa'
        '404':
          description: Pessoa não encontrada
        '500':
          description: Erro ao obter a pessoa
  /pessoas/{pessoa}:
    put:
      tags:
        - Pessoas
      summary: Atualiza uma pessoa
      operationId: 340e0612deef52b5517ef667e5dcf6ef
      parameters:
        - name: pessoa
          in: path
          description: Pessoa a ser atualizada
          required: true
          schema:
            type: integer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Pessoa'
      responses:
        '200':
          description: Pessoa atualizada com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Pessoa'
        '400':
          description: Erro de validação
        '500':
          description: Erro ao atualizar a pessoa
    delete:
      tags:
        - Pessoas
      summary: Deleta uma pessoa
      operationId: d0f995eb8bf727d7fd204f1d877f624d
      parameters:
        - name: pessoa
          in: path
          description: Pessoa a ser deletada
          required: true
          schema:
            type: integer
      responses:
        '204':
          description: Pessoa deletada com sucesso
        '500':
          description: Erro ao deletar a pessoa
  /relatorios/todas-pessoas:
    get:
      tags:
        - Relatórios
      summary: Relatório de todas as pessoas
      operationId: 2622d522649d9bfe832090cb3a83d740
      responses:
        '200':
          description: Relatório de todas as pessoas
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Pessoa'
        '500':
          description: Erro ao obter o relatório de todas as pessoas
  /relatorios/media-idade-genero:
    get:
      tags:
        - Relatórios
      summary: Relatório de média de idade por gênero
      operationId: 7d671edfd10c43d3a5199c7c8978af26
      responses:
        '200':
          description: Relatório de média de idade por gênero
          content:
            application/json:
              schema:
                properties:
                  homens:
                    type: array
                    items:
                      $ref: '#/components/schemas/Pessoa'
                  mulheres:
                    type: array
                    items:
                      $ref: '#/components/schemas/Pessoa'
                  mediaIdadeHomens:
                    type: number
                  mediaIdadeMulheres:
                    type: number
                type: object
        '500':
          description: Erro ao gerar o relatório de média de idade por gênero
  /relatorios/todos-veiculos:
    get:
      tags:
        - Relatórios
      summary: Relatório de todos os veículos
      operationId: 46eabc4eab78351401e1df6db49248ab
      responses:
        '200':
          description: Relatório de todos os veículos
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Veiculo'
        '500':
          description: Erro ao obter o relatório de todos os veículos
  /relatorios/veiculos-por-pessoa:
    get:
      tags:
        - Relatórios
      summary: Relatório de veículos por pessoa
      operationId: 771819ca230f54f42eb30cf9d4c31c2b
      responses:
        '200':
          description: Relatório de veículos por pessoa
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Veiculo'
        '500':
          description: Erro ao obter o relatório de veículos por pessoa
  /relatorios/contagem-por-genero:
    get:
      tags:
        - Relatórios
      summary: Relatório de contagem de veículos por gênero
      operationId: e468cec4d7f4ced0477d94fb39f3d3c7
      responses:
        '200':
          description: Relatório de contagem de veículos por gênero
          content:
            application/json:
              schema:
                type: array
                items:
                  properties:
                    contagemVeiculosHomens:
                      type: integer
                    contagemVeiculosMulheres:
                      type: integer
                    quemTemMaisVeiculos:
                      type: string
                  type: object
        '500':
          description: Erro ao gerar o relatório de contagem por gênero
  /relatorios/marcas-veiculos:
    get:
      tags:
        - Relatórios
      summary: Relatório de marcas de veículos
      operationId: b403487f8b2e363fa56321da4b744af4
      responses:
        '200':
          description: Relatório de marcas de veículos
          content:
            application/json:
              schema:
                properties:
                  marcasOrdenadasPorVeiculos:
                    type: array
                    items:
                      properties:
                        marca:
                          type: string
                        total:
                          type: integer
                      type: object
                  totaisMarcasHomens:
                    type: array
                    items:
                      properties:
                        marca:
                          type: string
                        total:
                          type: integer
                      type: object
                  totaisMarcasMulheres:
                    type: array
                    items:
                      properties:
                        marca:
                          type: string
                        total:
                          type: integer
                      type: object
                type: object
        '500':
          description: Erro ao gerar o relatório de marcas de veículos
  /relatorios/todas-revisoes:
    get:
      tags:
        - Relatórios
      summary: Relatório de todas as revisões
      operationId: f534575727de94bd95ed6f15446bdd49
      responses:
        '200':
          description: Relatório de todas as revisões
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/RevisaoVeicular'
        '500':
          description: Erro ao obter o relatório de todas as revisões
  /relatorios/marcas-maior-numero-revisoes:
    get:
      tags:
        - Relatórios
      summary: Relatório de marcas com maior número de revisões
      operationId: 17040b692dd5231d099e1f7de69be847
      responses:
        '200':
          description: Relatório de marcas com maior número de revisões
          content:
            application/json:
              schema:
                type: array
                items:
                  properties:
                    marca:
                      type: string
                    total:
                      type: integer
                  type: object
        '500':
          description: Erro ao obter o relatório de marcas com maior número de revisões
  /relatorios/pessoas-maior-numero-revisoes:
    get:
      tags:
        - Relatórios
      summary: Relatório de pessoas com maior número de revisões
      operationId: 7acaa4895e50c68777e93abb8c287a27
      responses:
        '200':
          description: Relatório de pessoas com maior número de revisões
          content:
            application/json:
              schema:
                type: array
                items:
                  properties:
                    pessoa_id:
                      type: integer
                    total:
                      type: integer
                  type: object
        '500':
          description: Erro ao obter o relatório de pessoas com maior número de revisões
  /relatorios/media-tempo-entre-revisoes/{pessoa_id}:
    get:
      tags:
        - Relatórios
      summary: Relatório de média de tempo entre revisões para uma pessoa
      operationId: 64daf8bf2085d0b8978cddd8f9f66c37
      parameters:
        - name: pessoa_id
          in: path
          description: ID da pessoa para a qual calcular a média de tempo entre revisões
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Relatório de média de tempo entre revisões
          content:
            application/json:
              schema:
                type: array
                items:
                  properties:
                    quantidadeRevisoes:
                      type: integer
                    mediaTempoEntreRevisoes:
                      type: integer
                    ultimaRevisaoData:
                      type: string
                    previsaoProximaRevisaoData:
                      type: string
                  type: object
        '500':
          description: Erro ao calcular a previsão de próxima revisão
  /veiculos/revisoes:
    get:
      tags:
        - RevisoesVeiculares
      summary: Lista todas as revisões veiculares
      operationId: 80a8c6c396fa877e880520bb94c49cd2
      responses:
        '200':
          description: Lista de todas as revisões veiculares
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/RevisaoVeicular'
        '500':
          description: Erro ao obter a lista de revisões veiculares
    post:
      tags:
        - RevisoesVeiculares
      summary: Cria uma nova revisão veicular
      operationId: ea6c14701a7f53af719de84b23da1ed0
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RevisaoVeicular'
      responses:
        '201':
          description: Revisão veicular criada com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/RevisaoVeicular'
        '400':
          description: Erro de validação
        '404':
          description: Veículo não encontrado
        '500':
          description: Erro ao criar uma nova revisão veicular
  /veiculos/revisoes/{id}:
    get:
      tags:
        - RevisoesVeiculares
      summary: Lista uma revisão veicular específica
      operationId: fc570ee3cf9937fbb903ba15f706dec4
      parameters:
        - name: id
          in: path
          description: ID da revisão veicular
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Revisão veicular encontrada
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/RevisaoVeicular'
        '404':
          description: Revisão veicular não encontrada
        '500':
          description: Erro ao obter a revisão veicular
  /veiculos/revisoes/{revisao}:
    put:
      tags:
        - RevisoesVeiculares
      summary: Atualiza uma revisão veicular
      operationId: 9f2bfc643bc32a2101f12b66907f4378
      parameters:
        - name: revisao
          in: path
          description: Revisão veicular a ser atualizada
          required: true
          schema:
            type: integer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RevisaoVeicular'
      responses:
        '200':
          description: Revisão veicular atualizada com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/RevisaoVeicular'
        '400':
          description: Erro de validação
        '500':
          description: Erro ao atualizar a revisão veicular
    delete:
      tags:
        - RevisoesVeiculares
      summary: Deleta uma revisão veicular
      operationId: 501c749d66da6274f9e488b113c1a79a
      parameters:
        - name: revisao
          in: path
          description: Revisão veicular a ser deletada
          required: true
          schema:
            type: integer
      responses:
        '204':
          description: Revisão veicular deletada com sucesso
        '500':
          description: Erro ao deletar a revisão veicular
  /veiculos:
    get:
      tags:
        - Veiculos
      summary: Lista todos os veículos
      operationId: 833f8b0fd14a8bc4e0cf2004898de4a2
      responses:
        '200':
          description: Lista de todos os veículos
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Veiculo'
        '500':
          description: Erro ao obter a lista de veículos
    post:
      tags:
        - Veiculos
      summary: Cria um novo veículo
      operationId: 813275f530859b8ff7ccd1e8c2d3b364
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Veiculo'
      responses:
        '201':
          description: Veículo criado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Veiculo'
        '400':
          description: Erro de validação
        '500':
          description: Erro ao criar um novo veículo
  /veiculos/{id}:
    get:
      tags:
        - Veiculos
      summary: Lista um veículo específico
      operationId: d9b5e2c1f60c68bc28fd37473ff04519
      parameters:
        - name: id
          in: path
          description: ID do veículo
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Veículo encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Veiculo'
        '404':
          description: Veículo não encontrado
        '500':
          description: Erro ao obter o veículo
  /veiculos/{veiculo}:
    put:
      tags:
        - Veiculos
      summary: Atualiza um veículo
      operationId: 7c798d033c9ad8e21cde13beb2e9a039
      parameters:
        - name: veiculo
          in: path
          description: Veículo a ser atualizado
          required: true
          schema:
            type: integer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Veiculo'
      responses:
        '200':
          description: Veículo atualizado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Veiculo'
        '400':
          description: Erro de validação
        '500':
          description: Erro ao atualizar o veículo
    delete:
      tags:
        - Veiculos
      summary: Deleta um veículo
      operationId: f8bdb6c66593a11962c5d10fd12ef74d
      parameters:
        - name: veiculo
          in: path
          description: Veículo a ser deletado
          required: true
          schema:
            type: integer
      responses:
        '204':
          description: Veículo deletado com sucesso
        '500':
          description: Erro ao deletar o veículo
components:
  schemas:
    Pessoa:
      title: Pessoa
      description: Pessoa model
      properties:
        '':
          title: Veículos
          description: Relacionamento com os veículos da pessoa
          type: array
          items:
            $ref: '#/components/schemas/Veiculo'
        fillable:
          title: ID
          description: ID da pessoa
          format: int64
      type: object
      xml:
        name: Pessoa
    RevisaoVeicular:
      title: RevisaoVeicular
      description: RevisaoVeicular model
      properties:
        veiculo:
          $ref: '#/components/schemas/Veiculo'
        pessoa:
          $ref: '#/components/schemas/Pessoa'
      type: object
      xml:
        name: RevisaoVeicular
    Veiculo:
      title: Veiculo
      description: Objeto de Veiculo
      properties:
        id:
          type: integer
        pessoa_id:
          type: integer
        marca:
          type: string
        tipo:
          type: string
        modelo:
          type: string
        placa:
          type: string
        pessoa:
          $ref: '#/components/schemas/Pessoa'
        revisoes:
          $ref: '#/components/schemas/RevisaoVeicular'
        fillable:
          title: ID
          description: ID do veículo
          format: int64
      type: object
tags:
  - name: Pessoas
    description: Operações relacionadas a pessoas
  - name: Relatórios
    description: Endpoints para relatórios
  - name: RevisoesVeiculares
    description: Operações relacionadas a revisões veiculares
  - name: Veiculos
    description: Operações relacionadas a veículos
