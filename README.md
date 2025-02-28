Assignment-1
from enum import Enum

# Enums for various statuses
class AccountStatus(Enum):
    ACTIVE = "active"
    INACTIVE = "inactive"
    LOCKED = "locked"

class OrderStatus(Enum):
    PLACED = "placed"
    SHIPPED = "shipped"
    DELIVERED = "delivered"

class PaymentStatus(Enum):
    SUCCESS = "success"
    FAILED = "failed"
    REFUNDED = "refunded"

class DeliveryStatus(Enum):
    PENDING = "pending"
    OUT_FOR_DELIVERY = "out_for_delivery"
    DELIVERED = "delivered"


# Customer Class
class Customer:
    def __init__(self, username, password, account_status):
        self.__username = username  # private
        self.__password = password  # private
        self.__account_status = account_status  # private

    # Getter for username
    def get_username(self):
        return self.__username

    # Setter for username
    def set_username(self, username):
        self.__username = username

    # Login method to validate account status
    def login(self):
        if self.__account_status == AccountStatus.ACTIVE:
            return f"Customer {self.__username} logged in successfully."
        else:
            return "Account is inactive. Please contact support."

    # String method to return object representation
    def __str__(self):
        return f"Customer(username={self.__username}, account_status={self.__account_status.value})"


# Order Class
class Order:
    def __init__(self, order_id, items, total_amount, status):
        self.__order_id = order_id  # private
        self.__items = items  # private
        self.__total_amount = total_amount  # private
        self.__status = status  # private

    # Getter and Setter for order_id
    def get_order_id(self):
        return self.__order_id

    def set_order_id(self, order_id):
        self.__order_id = order_id

    # Place the order
    def place_order(self):
        self.__status = OrderStatus.PLACED
        return f"Order {self.__order_id} has been placed."

    # Update order status
    def update_status(self, new_status):
        self.__status = new_status
        return f"Order {self.__order_id} status updated to {self.__status.value}."

    # String method to return object representation
    def __str__(self):
        return f"Order(order_id={self.__order_id}, items={self.__items}, total_amount={self.__total_amount}, status={self.__status.value})"


# Payment Class
class Payment:
    def __init__(self, payment_id, payment_method, amount, status):
        self.__payment_id = payment_id  # private
        self.__payment_method = payment_method  # private
        self.__amount = amount  # private
        self.__status = status  # private

    # Process payment
    def process_payment(self):
        if self.__status == PaymentStatus.SUCCESS:
            return f"Payment {self.__payment_id} processed successfully."
        else:
            return "Payment failed. Please try again."

    # Refund method
    def refund(self):
        if self.__status == PaymentStatus.SUCCESS:
            self.__status = PaymentStatus.REFUNDED
            return f"Payment {self.__payment_id} has been refunded."
        else:
            return "Refund cannot be processed."

    # String method to return object representation
    def __str__(self):
        return f"Payment(payment_id={self.__payment_id}, payment_method={self.__payment_method}, amount={self.__amount}, status={self.__status.value})"


# Delivery Class
class Delivery:
    def __init__(self, delivery_id, delivery_status, estimated_time):
        self.__delivery_id = delivery_id  # private
        self.__delivery_status = delivery_status  # private
        self.__estimated_time = estimated_time  # private

    # Track delivery status
    def track_delivery(self):
        return f"Delivery {self.__delivery_id} is {self.__delivery_status.value}. Estimated delivery time: {self.__estimated_time}."

    # Assign delivery agent
    def assign_agent(self, agent_name):
        return f"Delivery {self.__delivery_id} has been assigned to {agent_name}."

    # String method to return object representation
    def __str__(self):
        return f"Delivery(delivery_id={self.__delivery_id}, delivery_status={self.__delivery_status.value}, estimated_time={self.__estimated_time})"


# Example of creating objects and testing

# Create objects
customer1 = Customer("Ahmed Ali", "password123", AccountStatus.ACTIVE)
order1 = Order("ORD1245", ["item1", "item2"], 250.00, OrderStatus.PLACED)
payment1 = Payment("PAY12345", "credit_card", 250.00, PaymentStatus.SUCCESS)
delivery1 = Delivery("DEL12345", DeliveryStatus.OUT_FOR_DELIVERY, "2:00 PM")

# Call methods and print object representations
print(customer1)
print(order1.place_order())
print(payment1.process_payment())
print(delivery1.track_delivery())

# Update and print updated objects
order1.update_status(OrderStatus.SHIPPED)
print(order1)

# Print individual method outputs
print(customer1.login())
print(payment1.refund())
print(delivery1.assign_agent("Agent A"))
