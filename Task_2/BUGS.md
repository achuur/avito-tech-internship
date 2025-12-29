# Баг-репорты по заданию 2.1:

### **1. При успешном создании объявления в ответе приходит только status**
  
    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
    {
    "sellerID": {{randomNumber}},
    "name": "title",
    "price": {{$randomInt}},
    "statistics": {
        "likes": {{$randomInt}},
        "viewCount": {{$randomInt}},
        "contacts": {{$randomInt}}
     }
    }

    **Ожидаемый результат:**
    Статус-код 200, структура тела ответа:
    {
    id: { type: string }
    sellerId: { type: integer }
    name: { type: string }
    price: { type: integer }
    createdAt: { type: string }
    statistics: {
        likes: { type: integer }
        viewCount: { type: integer }
        contacts: { type: integer }
                  }
    }

    **Фактический результат:**
    Статус-код 200, тело ответа:
    {
    "status": {type: string}
    }

### **2. Поле sellerID принимает отрицательные значения**

    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
  {
  "sellerID": -11,
  "name": "title",
  "price": 250,
  "statistics": {
    "likes": 83,
    "viewCount": 976,
    "contacts": 342
    }
   }   

   **Ожидаемый результат:**
   Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   additionalProperties: {type: string}
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    {
    status: {type: string}
    }

### **3. Поле price принимает отрицательные значения**

    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
 {
  "sellerID": 11,
  "name": "title",
  "price": -250,
  "statistics": {
    "likes": 83,
    "viewCount": 976,
    "contacts": 342
  }
 }     

   **Ожидаемый результат:**
   Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   additionalProperties: {type: string}
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    {
    status: {type: string}
    }

### **4. Поле likes принимает отрицательные значения**

    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
 {
  "sellerID": 11,
  "name": "title",
  "price": 250,
  "statistics": {
    "likes": -83,
    "viewCount": 976,
    "contacts": 342
  }
 }       

   **Ожидаемый результат:**
   Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   additionalProperties: {type: string}
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    {
    status: {type: string}
    }

### **5. Поле viewCount принимает отрицательные значения**

    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
 {
  "sellerID": 11,
  "name": "title",
  "price": 250,
  "statistics": {
    "likes": 83,
    "viewCount": -976,
    "contacts": 342
  }
 }   

   **Ожидаемый результат:**
   Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   additionalProperties: {type: string}
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    {
    status: {type: string}
    }

### **6. Поле contacts принимает отрицательные значения**

    **Шаги воспроизведения:**
    Отправить запрос POST /api/1/item с телом:
 {
  "sellerID": 11,
  "name": "title",
  "price": 250,
  "statistics": {
    "likes": 83,
    "viewCount": 976,
    "contacts": -342
  }
 }   

   **Ожидаемый результат:**
   Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    {
    status: {type: string}
    }

### **7. При вводе несуществующего sellerID получаем успешный ответ с пустым массивом**

    **Шаги воспроизведения:**
    Отправить запрос GET /api/1/:sellerID/item, с Path-параметром:
    sellerID: 8

    **Ожидаемый результат:**
    Статус-код 400, структура тела ответа:
   {
   result: {
            message: {type: string}
            messages: {type: object}
            }
   }

   **Фактический результат:**
   Статус-код 200, тело ответа:
    []
    
