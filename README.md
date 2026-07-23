# QuimEdu-Lab

Plataforma educacional para Química e Bioquímica Aplicada.

## Sobre

QuimEdu-Lab é um projeto dedicado ao ensino prático de química e bioquímica, com foco em aplicações reais e relevantes. Desenvolvemos ferramentas, tutoriais e simulações para facilitar o aprendizado usando bibliotecas profissionais de química.

## Objetivos

- Criar ferramentas educacionais em química molecular
- Desenvolver calculadoras para reações químicas
- Disponibilizar simulações interativas
- Publicar tutoriais de bioquímica aplicada
- Construir comunidade de aprendizagem

## Funcionalidades

- Manipulação de estruturas moleculares (RDKit)
- Análise de proteínas e bioquímica (Biotite)
- Simulação de reações químicas (ChemPy)
- Base de dados de compostos
- Análise de estruturas 3D
- Cálculos de propriedades moleculares

## Tecnologias

- **RDKit**: Química computacional e manipulação molecular
- **Biotite**: Análise de proteínas e bioquímica
- **ChemPy**: Simulações de reações químicas
- **Python 3.8+**: Linguagem de programação

## Como Começar

### Pré-requisitos

- Python 3.8 ou superior
- pip (gerenciador de pacotes Python)

### Instalação

```bash
git clone https://github.com/TTMOR/QuimEdu-Lab.git
cd QuimEdu-Lab
pip install -r requirements.txt
```

### Dependências

```bash
pip install rdkit-pypi
pip install biotite
pip install chempy
pip install numpy
pip install pandas
pip install matplotlib
```

## Uso Básico

### Exemplo 1: Análise de Moléculas com RDKit

```python
from rdkit import Chem
from rdkit.Chem import Descriptors, AllChem

# Criar molécula a partir de SMILES
smiles = "CC(=O)Oc1ccccc1C(=O)O"  # Ácido acetilsalicílico (Aspirina)
mol = Chem.MolFromSmiles(smiles)

# Calcular propriedades
peso_molecular = Descriptors.MolWt(mol)
logp = Descriptors.MolLogP(mol)
hbd = Descriptors.NumHDonors(mol)
hba = Descriptors.NumHAcceptors(mol)

print(f"Peso Molecular: {peso_molecular} g/mol")
print(f"LogP: {logp}")
print(f"H-Bond Donors: {hbd}")
print(f"H-Bond Acceptors: {hba}")
```

### Exemplo 2: Estrutura de Proteína com Biotite

```python
import biotite.structure as struc
import biotite.structure.io.pdb as pdb

# Carregar estrutura de proteína (PDB)
pdb_file = pdb.PDBFile.read("1MBN.pdb")
structure = pdb_file.get_structure()

# Informações básicas
print(f"Número de átomos: {structure.array_length()}")
print(f"Número de resíduos: {len(struc.get_residues(structure))}")

# Calcular distância entre dois átomos
coord_ca = structure.coord[structure.atom_name == "CA"]
print(f"Coordenadas Alpha Carbons (primeiros 5):\n{coord_ca[:5]}")
```

### Exemplo 3: Simulação de Reação com ChemPy

```python
from chempy import Reaction, Substance
from chempy.kinetics.util import solve_odesys

# Definir reação: 2A + B -> C
# Criar substâncias
A = Substance.latex_name("A", r"\ce{A}")
B = Substance.latex_name("B", r"\ce{B}")
C = Substance.latex_name("C", r"\ce{C}")

# Definir reação
rxn = Reaction({"A": 2, "B": 1}, {"C": 1}, inact_reac={"A": A, "B": B, "C": C})

# Parâmetros
k = 0.1  # constante de velocidade
y0 = {"A": 1.0, "B": 1.0, "C": 0.0}  # condições iniciais
t = [0, 1, 2, 5, 10]  # tempos

# Resolver sistema
result = solve_odesys(rxn, y0, k, t)
print(result)
```

### Exemplo 4: Propriedades Moleculares

```python
from rdkit import Chem
from rdkit.Chem import Crippen, Descriptors

# Moléculas de exemplo
smiles_list = {
    "Agua": "O",
    "Etanol": "CCO",
    "Benzeno": "c1ccccc1",
    "Cafeina": "CN1C=NC2=C1C(=O)N(C(=O)N2C)C"
}

for nome, smiles in smiles_list.items():
    mol = Chem.MolFromSmiles(smiles)
    if mol:
        print(f"\n{nome}: {smiles}")
        print(f"  Peso Molecular: {Descriptors.MolWt(mol):.2f}")
        print(f"  Solubilidade (LogP): {Crippen.MolLogP(mol):.2f}")
        print(f"  Número de Átomos: {mol.GetNumAtoms()}")
        print(f"  Fórmula Molecular: {Chem.rdMolDescriptors.CalcMolFormula(mol)}")
```

## Estrutura do Projeto

```
QuimEdu-Lab/
├── docs/                  # Documentação
├── src/
│   ├── molecular/         # Análise molecular (RDKit)
│   ├── protein/           # Estruturas proteicas (Biotite)
│   ├── reactions/         # Simulações de reações (ChemPy)
│   └── utils/             # Utilitários
├── examples/              # Exemplos completos
├── tests/                 # Testes unitários
├── requirements.txt       # Dependências
└── README.md
```

## Contribuindo

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/minha-feature`)
3. Commit suas mudanças (`git commit -m "Adiciona minha feature"`)
4. Push para a branch (`git push origin feature/minha-feature`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo LICENSE para detalhes.

## Autores

TTMOR

## Contato

Para dúvidas, sugestões ou contribuições, abra uma issue ou entre em contato através do GitHub.

## Recursos Adicionais

- RDKit Documentation: https://www.rdkit.org/docs/
- Biotite Documentation: https://www.biotite-python.org/
- ChemPy Documentation: https://chempython.readthedocs.io/
- Python: https://docs.python.org
