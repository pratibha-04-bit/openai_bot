from django.test import TestCase
from phoenix_NA.models import *

class ClientTestCase(TestCase):
    def setUp(self):
        self.client_name = "Test Client"
        self.address = "123 Test St"
        self.timezone = "UTC"
        self.website = "http://example.com"
        self.industry = "Test Industry"
        self.size = "Small"

        self.client = Client.objects.create(
            name=self.client_name,
            address=self.address,
            timezone=self.timezone,
            website=self.website,
            industry=self.industry,
            size=self.size
        )

    def test_client_creation(self):
        client = Client.objects.get(name=self.client_name)
        self.assertEqual(client.address, self.address)
        self.assertEqual(client.timezone, self.timezone)
        self.assertEqual(client.website, self.website)
        self.assertEqual(client.industry, self.industry)
        self.assertEqual(client.size, self.size)

    def test_client_update(self):
        new_address = "456 New St"
        new_timezone = "PST"
        new_website = "http://newexample.com"
        new_industry = "New Industry"
        new_size = "Medium"

        self.client.address = new_address
        self.client.timezone = new_timezone
        self.client.website = new_website
        self.client.industry = new_industry
        self.client.size = new_size
        self.client.save()

        updated_client = Client.objects.get(name=self.client_name)
        self.assertEqual(updated_client.address, new_address)
        self.assertEqual(updated_client.timezone, new_timezone)
        self.assertEqual(updated_client.website, new_website)
        self.assertEqual(updated_client.industry, new_industry)
        self.assertEqual(updated_client.size, new_size)



class ContactsTestCase(TestCase):
    def setUp(self):
        self.client = Client.objects.create(
            name="Test Client",
            address="123 Test St",
            timezone="UTC",
            website="http://example.com",
            industry="Test Industry",
            size="Small"
        )
        self.contact_name = "Test Contact"
        self.email = "test@example.com"
        self.phone = "123-456-7890"
        self.mobile = "987-654-3210"
        self.role = "Test Role"
        self.title = "Test Title"
        self.status = "Active"

        self.contact = Contacts.objects.create(
            client=self.client,
            name=self.contact_name,
            email=self.email,
            phone=self.phone,
            mobile=self.mobile,
            role=self.role,
            title=self.title,
            status=self.status
        )

    def test_contact_creation(self):
        contact = Contacts.objects.get(name=self.contact_name)
        self.assertEqual(contact.email, self.email)
        self.assertEqual(contact.phone, self.phone)
        self.assertEqual(contact.mobile, self.mobile)
        self.assertEqual(contact.role, self.role)
        self.assertEqual(contact.title, self.title)
        self.assertEqual(contact.status, self.status)

    def test_contact_update(self):
        new_email = "new_test@example.com"
        new_phone = "111-222-3333"
        new_mobile = "999-888-7777"
        new_role = "New Role"
        new_title = "New Title"
        new_status = "Inactive"

        self.contact.email = new_email
        self.contact.phone = new_phone
        self.contact.mobile = new_mobile
        self.contact.role = new_role
        self.contact.title = new_title
        self.contact.status = new_status
        self.contact.save()

        updated_contact = Contacts.objects.get(name=self.contact_name)
        self.assertEqual(updated_contact.email, new_email)
        self.assertEqual(updated_contact.phone, new_phone)
        self.assertEqual(updated_contact.mobile, new_mobile)
        self.assertEqual(updated_contact.role, new_role)
        self.assertEqual(updated_contact.title, new_title)
        self.assertEqual(updated_contact.status, new_status)

    # def test_contact_deletion(self):
    #     self.contact.delete()
    #     with self.assertRaises(Contacts.DoesNotExist):
    #         Contacts.objects.get(name=self.contact_name)
