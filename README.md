# android-chat-heads
A facebook like chat heads library for android apps. This includes all the UI physics and spring animations which drive multi user chat behaviour and toggling between maximized and minimized modes.



# Integration

The view adapter is invoked when someone selects a chat head.
In this example I have attached a <String> object to each chat head using generics. You can attach any object, for e.g <Conversation> object to denote each chat head.
This object will be passed in all callbacks.

        final ChatHeadContainer chatContainer = (ChatHeadContainer) findViewById(R.id.chat_container);
        chatContainer.setViewAdapter(new ChatHeadViewAdapter() {
            @Override
            public FragmentManager getFragmentManager() {
                return getSupportFragmentManager();
            }

            @Override
            public Fragment getFragment(Object key, ChatHead chatHead) {
                return new Fragment();
            }

            @Override
            public Drawable getChatHeadDrawable(Object key) {
                return getResources().getDrawable(R.drawable.circular_view);
            }
        });
        chatContainer.setOnItemSelectedListener(new ChatHeadContainer.OnItemSelectedListener() {
            @Override
            public boolean onChatHeadSelected(Object key, ChatHead chatHead) {
                if (chatContainer.getArrangementType() == CircularArrangement.class) {
                    System.out.println("Clicked on " + key + " " +
                            "when arrangement was circular");
                }
                chatContainer.setArrangement(MaximizedArrangement.class, null);
                return true;
            }
        });
        chatContainer.addChatHead("head0", false);
        chatContainer.addChatHead("head1", false);
        Button addButton = (Button) findViewById(R.id.add);
        Button removeButton = (Button) findViewById(R.id.remove);
        addButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                chatContainer.addChatHead("head" + Math.random(), false);
            }
        });
        removeButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Set<Object> keys = chatContainer.getChatHeads().keySet();
                Object[] objects = keys.toArray();
                if (objects.length > 0) {
                    Object object = objects[objects.length - 1];
                    chatContainer.removeChatHead(object);
                }
            }
        });
