# 📚 Trabalho - Design Tático no DDD

## 📌 Objetivo
Criar as **Entidades, Value Objects, Agregados e Repositórios** do seu projeto, aplicando o **Design Tático do DDD**.

---

## 📂 **1️⃣ Conceitos Fundamentais**

### **🧩 Entidades vs. Objetos de Valor**
📌 **Entidades** têm **identidade única** e podem mudar ao longo do tempo.  
📌 **Objetos de Valor** não possuem identidade própria e são **imutáveis**.  

💡 **Exemplo no Contexto de Consultas Médicas:**  

| **Elemento**      | **Entidade ou Value Object?** | **Justificativa** |
|------------------|-----------------------------|-------------------|
| **Locatário**     | Entidade                     | Tem um ID único e pode mudar seus dados ao longo do tempo. |
| **Locador**       | Entidade                     | Possui identidade única. |
| **Endereço**     | Value Object                 | Se um locador ou locatário muda de endereço, não faz sentido modificar o antigo, apenas substituí-lo. |
| **CPF**          | Value Object                 | Sempre pertence a apenas um usuário (locatário e locador) e não muda. |

---

### **🏗️ Agregados e Aggregate Root**
- Um **Agregado** agrupa entidades e objetos de valor que fazem parte de uma mesma regra de consistência.  
- O **Aggregate Root** é a entidade principal que controla a consistência do agregado.  

📌 **Exemplo de Agregado para o Contexto de Consultas Médicas:**  
- **Consulta** (Aggregate Root)  
  - Médico (Entidade)  
  - Paciente (Entidade)  
  - Data da Consulta (Value Object)  
  - Diagnóstico (Value Object)  

📌 **Regras de Negócio no Agregado:**  
- Um **médico** só pode ter **uma consulta ativa por horário**.  
- Uma **consulta finalizada** não pode ser alterada.  

---

### **🗃️ Repositórios**
Os **Repositórios** são responsáveis por **persistir e recuperar** agregados.  
✅ Devem **trabalhar apenas com Aggregate Roots**.  
✅ **Não devem expor entidades internas do agregado diretamente**.  

💡 **Exemplo de Interface de Repositório para o Contexto de Consultas:**  

```csharp
public interface IAluguelRepository
{
    Aluguel ObterPorId(Guid id);
    void Salvar(Aluguel aluguel);
}
```

📌 **Por que o Repositório trabalha apenas com `Consulta`?**  
- Porque **Consulta é o Aggregate Root**, então **Paciente e Médico são gerenciados por ele**.  

---

## **📝 2️⃣ Atividade Prática: Modelagem do Domínio**

📌 **Objetivo:**  
Criar as **Entidades, Value Objects, Agregados e Repositórios** do seu projeto.  

📌 **Instruções:**  
1️⃣ **Identifique as Entidades e Value Objects** do seu domínio.  
2️⃣ **Defina os Agregados e seu Aggregate Root**.  
3️⃣ **Implemente um diagrama mostrando as relações entre os elementos**.  
4️⃣ **Crie a interface do repositório para persistência do agregado**.  

📌 **Exemplo de Resposta para Keller’s Health:**  

| **Elemento**            | **Tipo**         | **Explicação** |
|-------------------------|-----------------|---------------|
| Locatário               | Entidade        | Possui identidade única e pode mudar ao longo do tempo. |
| Locador                 | Entidade        | Tem uma identidade única. |
| CPF                    | Value Object    | Não muda e sempre pertence a um único usuário. |
| Endereço               | Value Object    | Se o locatário ou locador mudar de endereço, um novo objeto será criado. |
| Aluguel (Agregado)    | Aggregate Root  | Controla a relação entre Locatário, Locador e Data do Aluguel. |


📌 **Ferramentas para Criar o Diagrama:**  
- [Miro](https://miro.com/)  
- [Lucidchart](https://www.lucidchart.com/)  
- [Figma](https://www.figma.com/)  
