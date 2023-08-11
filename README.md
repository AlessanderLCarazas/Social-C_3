# Social-C_3
# Sistema Social-C

# 1. Principios SOLID
### 1.1 Principio de Responsabilidad Única

Es el principio SOLID más aplicable a las funciones proporcionadas en tu código. Cada función tiene una única responsabilidad y está enfocada en una tarea específica:

createMessage: Responsable de crear un nuevo mensaje en un chat.
getMessages: Responsable de obtener todos los mensajes de un chat específico.
Estas funciones cumplen con el principio de realizar una sola tarea y tener una única razón para cambiar. Cada función tiene un propósito claro y está limitada a esa responsabilidad.

```jsx
const messageModel = require("../Models/messageModel");


// createriessage
const createMessage = async (req, res) => {
    const { chatId, senderId, text } = req.body;

    const message = new messageModel ({
        chatId,
        senderId,
        text,
    });

    try {
        const response = await message.save();
        res.status(200).json(response);
    } catch (error) {
        console.log(error);
        res.status(500).json(error);
    }
};

// getMessages
const getMessages = async (req, res) => {
    const { chatId } = req.params;

    try {
        const messages = await messageModel.find({ chatId });
        res.status(200).json(messages);
    } catch (error) {
        console.log(error);
        res.status(500).json(error);   
    }
};

module.exports = { createMessage, getMessages};
```

### 1.2 Principio de Abierto/Cerrado (OCP):
El principio de abierto/cerrado se aplica directamente aquí. Este fragmento de código define un esquema de modelo específico y lo crea utilizando mongoose. Sin embargo, podría argumentarse que este fragmento es "cerrado para modificación" ya que encapsula la definición del modelo y la creación en una única unidad que se puede utilizar en otras partes del código sin necesidad de modificarlo directamente.

```jsx
const mongoose = require("mongoose")

const userSchema = new mongoose.Schema(
    {
        name: {type: String, required: true, minlength: 3, maxlength: 30},
        email: {
            type: String,
            required: true,
            minlength: 3,
            maxlength: 200,
            unique: true
        },
        password: {type: String, required: true, minlength: 3, maxlength: 1024},
    },
    {
        timestamps: true,
    }
);

const userModel = mongoose.model("User", userSchema)

module.exports = userModel
```

Trello: https://trello.com/b/pvwoTADC/social-c-is-i

![image](https://github.com/AlessanderLCarazas/Social-C_3/assets/104175707/6ce8c474-c29a-452f-8224-94b1a437cf23)




