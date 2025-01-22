'''
@Component
@Slf4j
public class ReadRukiaOvO extends ReadMeHandler
{
    private AsyncExecutor executor;
    private MusicPlayer musicPlayer;

    @Autowired
    public ReadRukiaOvO(AsyncExecutor executor, MusicPlayer musicPlayer)
    {
        this.executor = executor;
        this.musicPlayer = musicPlayer;
    }

    @SneakyThrows
    @Override
    public void onReadMe(@NonNull ReadMeSession session)
    {
        log.info("Someone is reading README.md.");
        if(session.getWannaOrNot().equals("not")) {return;}
        
        CompletableFuture.runAsync(() -> musicPlayer.On("On My Own - Blitz kids"), executor);
        RukiaOvO me = new RukiaOvO.builder()
                               .programmingLanguage(List.of("Java", "Go"))
                               .country("China/PRC")
                               .languages(new HashMap<String, Proficiency>() {{
                                   put("Chinese", Proficiency.NATIVE);
                                   put("English", Proficiency.UNDERSTANDING);
                               }})
                               .selfDescription("A noob in learning Java/Go.")
                               .build();
        session.sendReadMeMsg(JSON.toJSONString(me));
    }
}

'''
