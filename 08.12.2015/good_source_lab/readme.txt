���� ������ - ����� ������������

���������� ������ ��������� ������ ��������� ��������.
������ ��������� ������� � ������� �� ����� �������. ������� ������������� ������������ ������� RemotingConfiguration.RegisterWellKnownServiceType �� ������� �������.
SingleCall	������ �������� ��������� ������������� ����� ����������� �������.
Singleton	������ �������� ��������� ������������� ��� �� ����������� �������.


namespace RemoteHello
{
    public class ChatServerObject : System.MarshalByRefObject
    { 
        // Fields
        private ArrayList clients = new ArrayList(); // Names of clients
        private String chatSession = ""; // Holds text for chat session
        public void AddClient(string name) 
        {
            if (name != null) 
            {
                lock (clients)
                {
                    clients.Add(name);
                }
            }
        }
        public void RemoveClient(String name) 
        {
            lock (clients) 
            {
                clients.Remove(name);
            }
        }
        public void AddText(String newText) 
        {
            if (newText != null)
            {
                lock (chatSession)
                {
                    if (chatSession == "")
                        chatSession += newText;
                    else  chatSession +=Environment.NewLine + newText;
                }
            }
        }
        public ArrayList Clients() 
        {
            return clients;
        }
        public String ChatSession() 
        {
            return chatSession;
        }
    }
}